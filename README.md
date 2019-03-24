# Patterns Sampling in Distributed Databases

To run DDSamplingRDF.jar, one want to unzip the DDSamplingRDF.rar file. The fold that we will obtain contains the jar file and another fold "Output". In this folder, we have the weighting matrix that we used to sample pattern from the distributed database (DBpedia+Wikidata). Now with the command line, move into the DDSamplingRDF folder (<i>DDSamplingRDF/</i>) and run one of the following requests.<br>
The main syntax is : <br>
	java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:<sample size> M:<maximum length constrain> B:<database> U:<utility> d:<decay if U:Decay>
	Example :
	java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Frea
	or
	java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Decqy d:0.025

If the user can :
-	do classification with the sample pattern by adding Classif:Y. If Classif:N, then there are no classifcation task
	Example :
	java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:3 B:DW U:Area Classif:N
-	repeat the job n times by adding : nbRep:<n>
	Example :
	java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:2 B:DW U:Freq Classif:N nbRep:10
-	restrict the number of entities per class that he want to use in order to decrease the input dataset by adding NEC:<value>
	Example :
	java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Freq NEC:1000

If the weighting matrix is not yet built, DDSamplingRDF want to build the weighting matrix by requested the triplestores. We allow user to draw a sample from the entities with a type (or class) having at least k entities by adding minNEC:<k>
	Example :
	java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Freq NEC:1000 minNEC:3000

When one want to draw a sample from a single fragment, he must specify it (D for DBpedia, W for Wikidata).
	java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:D U:Area
	or
	java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:W U:Area

