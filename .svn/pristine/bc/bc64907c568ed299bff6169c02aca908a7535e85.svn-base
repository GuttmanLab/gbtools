package broad.pda.rnaseq.misc;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Collection;
import java.util.HashMap;
import java.util.Iterator;
import java.util.List;
import java.util.Map;
import java.util.TreeMap;
import java.util.TreeSet;

import broad.core.datastructures.IntervalTree;
import broad.core.datastructures.IntervalTree.Node;
import broad.core.motif.SearchException;
import broad.core.motif.SequenceMotif;
import broad.core.sequence.Sequence;
import broad.core.sequence.SequenceRegion;
import broad.pda.annotation.BEDFileParser;
import broad.pda.chromosome.Chromosome;
import broad.pda.datastructures.Alignments;
import broad.pda.gene.RefSeqGene;
import broad.pda.rnai.ExtractSequence;
import broad.pda.rnai.designer.ComputeMIRScore;

public class FindNumberOfGraphsPerGene {

	public static void main(String[] args)throws Exception{
		if(args.length == 2){
			Map<String, Collection<RefSeqGene>> genesByChr=BEDFileParser.loadDataByChr(new File(args[0]));
			Map<String, Collection<RefSeqGene>> reconstructionsByChr=BEDFileParser.loadDataByChr(new File(args[1]));
			for(String chr : reconstructionsByChr.keySet()) {
				IntervalTree<RefSeqGene> chrTree = new IntervalTree<RefSeqGene>();
				Collection<RefSeqGene> chrReconstructions = reconstructionsByChr.get(chr);
				for(RefSeqGene g : chrReconstructions) {
					chrTree.put(g.getStart(), g.getEnd(),g);
				}
				
				Collection<RefSeqGene> chrGenes = genesByChr.get(chr);
				for(RefSeqGene g : chrGenes) {
					Iterator<Node<RefSeqGene>> gReconstructions = chrTree.overlappers(g.getStart(), g.getEnd());
					int num = 0;
					while(gReconstructions.hasNext()) {
						gReconstructions.next();
						num++;
					}
					
					System.out.println(g.getName()+ "\t" + num + "\n");
				}
 			}
		}
		else{System.err.println(usage);}
	}
	
	static String usage=" args[0]=genes \n args[1]=reconstructions";
	
}
