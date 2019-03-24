<h1>Patterns Sampling in Distributed Databases</h1>

To run <b>DDSamplingRDF.jar</b>, one want to unzip the DDSamplingRDF.rar file. The fold that we will obtain contains the jar file and another fold <b>Output</b>. In this folder, we have the weighting matrix (<b>matPond</b>) that we used to sample pattern from the distributed database (<b>DBpedia+Wikidata</b>). Now with the command line, move into the DDSamplingRDF folder (<i>DDSamplingRDF/</i>) and run one of the following requests.<br>
The main syntax is : <br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar <b>N</b>:\<sample size\> <b>M</b>:\<maximum length constrain\> <b>B</b>:\<database\> <b>U</b>:\<utility\> <b>d</b>:\<decay value if U:Decay\></i><br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Frea</i><br>
	or <br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Decay d:0.025</i><br>

The user can :
-	do classification with the sample pattern by adding <b>Classif</b>:<font color="lime">Y</font>. If <b>Classif</b>:<font color="#ff0000">N</font>, then there are no classifcation task<br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:3 B:DW U:Area <b>Classif</b>:<font color="red">N</font></i><br>
-	repeat the job <i>n</i> times by adding : <b>nbRep</b>:<n><br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:2 B:DW U:Freq Classif:N <b>nbRep</b>:10</i><br>
-	restrict the number of entities per class that he want to use in order to decrease the input dataset by adding <b>NEC</b>:<value><br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Freq <b>NEC</b>:1000</i><br>

If the weighting matrix is not yet built, DDSamplingRDF want to build q first the weighting matrix by requested the triplestores. We allow user to draw an input sample from the entities with a type (or class) having at least <i>k</i> entities by adding <b>minNEC</b>:<k><br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Freq NEC:1000 <b>minNEC</b>:3000</i><br>

When one want to draw a sample from a single fragment, he must specify it (<d>D</d> for DBpedia, <d>W<?d> for Wikidata).<br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:<b>D</b> U:Area</i> <br>
	or<br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:<b>W</b> U:Area</i>

