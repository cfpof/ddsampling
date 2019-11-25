<h1>Patterns Sampling in Distributed Databases</h1>

To run <b>DDSamplingRDF.jar</b>, one want to unzip the DDSamplingRDF.rar file. The fold that we will obtain contains the jar file and another fold <b>Output</b>. In this folder, we have the weighting matrix (<b>matPond_C</b>, where <b>C</b> is the class) that we used to sample pattern from the distributed database (<b>DBpedia+Wikidata</b>). To do some simulation with the existing benchmarks, we use also some distributed local databases as mentioned in the paper.
So we have folders that contain these distributed databases partitioned by ourselves from the UCI repository.
Now with the command line, move into the DDSamplingRDF folder (<i>DDSamplingRDF/</i>) and run one of the following requests.<br>
The main syntax is : <br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingPAKDD20.jar <b>online:no</b> <b>sampleSize</b>:\<sample size\> <b>utility</b>:\<Freq or Area\> <b>dataset</b>:\<"connect" for example\> <b>maxLength</b>:\<maximal length constraint\> <b>pType</b>:\<partitioning type VL, HL, HD\> <b>nbSites</b>:\<number of sites\> <b>nbFailedSites</b>:\<number of failed sites\> <b>errorRate</b>:\<error rate\> <b>recordSample</b>:\<Yes or No for reccording the sampled patterns\> </i><br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Freq</i><br>
	or <br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Decay d:0.025</i><br>
	
	<iframe name="lesteph" src="" width="468" height="60" marginwidth="0" marginheight="0" hspace="0" vspace="0" frameborder="0" scrolling="no">
	
	java "-Dfile.encoding=UTF-8" -jar DDSamplingPAKDD20.jar online:no sampleSize:1000 utility:Freq dataset:connect maxLength:3 pType:VL nbSites:10 nbFailedSites:0 errorRate:0.0 recordSample:No
DDSampling on local distributed database : connect
Running with parameters :
        Max length : 3
        Utility : Freq
        Sample size : 1000
        Partition type : VL
Preprocessing time (s) : 3.483
Total number of instances : 67557
Rejection rate : 0.0
Sampling time (s) : 0.019
*********** END ***************

java "-Dfile.encoding=UTF-8" -jar DDSamplingPAKDD20.jar online:no sampleSize:1000 utility:Freq dataset:connect maxLength:3 pType:HL nbSites:10 nbFailedSites:0 errorRate:0.0 recordSample:Yes
DDSampling on local distributed database : connect
Running with parameters :
        Max length : 3
        Utility : Freq
        Sample size : 1000
        Partition type : HL
Preprocessing time (s) : 2.27
Total number of instances : 67557
Rejection rate : 0.0
Please recover your sample from :
OutputPatternsLocalDatabases/Freq/HL/connect/connect1000N1m3M0z0_0p.TXT
Sampling time (s) : 0.04
*********** END ***************
	
	</iframe>

The user can :
-	do classification with the sampled patterns by adding <b>Classif</b>:<font color="lime">Y</font>. If <b>Classif</b>:<font color="#ff0000">N</font>, then there is no classifcation task<br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:3 B:DW U:Area <b>Classif</b>:<font color="red">N</font></i><br>
-	repeat the job <i>n</i> times by adding : <b>nbRep</b>:\<n\><br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:2 B:DW U:Freq Classif:N <b>nbRep</b>:10</i><br>
-	restrict the number of entities per class that he want to use in order to decrease the input dataset by adding <b>NEC</b>:\<value\><br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Freq <b>NEC</b>:1000</i><br>

If the weighting matrix is not yet built, DDSamplingRDF want a first to build it by requesting the triplestores. We allow user to draw an input sample from the entities with a type (or class) having at least <i>k</i> entities by adding <b>minNEC</b>:\<k\><br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:DW U:Freq NEC:1000 <b>minNEC</b>:3000</i><br>

When one want to draw a sample from a single fragment, he must specify it (<b>D</b> for DBpedia, <b>W</b> for Wikidata).<br>
	<b>Example :</b><br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:<b>D</b> U:Area</i> <br>
	or<br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingRDF.jar N:1000 M:10 B:<b>W</b> U:Area</i>
<br><br>
To find the <b>sampled patterns</b>, check the <b>Output</b> folder.
