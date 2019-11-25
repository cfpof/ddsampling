<h1>Patterns Sampling in Distributed Databases</h1>

To run <b>DDSamplingRDF.jar</b>, one want to unzip the DDSamplingRDF.rar file. The fold that we will obtain contains the jar file and another fold <b>Output</b>. In this folder, we have the weighting matrix (<b>matPond_C</b>, where <b>C</b> is the class) that we used to sample pattern from the distributed database (<b>DBpedia+Wikidata</b>). To do some simulation with the existing benchmarks, we use also some distributed local databases as mentioned in the paper.
So we have folders that contain these distributed databases partitioned by ourselves from the UCI repository.
Now with the command line, move into the DDSamplingRDF folder (<i>DDSamplingRDF/</i>) and run one of the following requests.<br> In our experiments, we distinguished two cases: 

	(1) The database is distributed but stored locally. 
	(2) The database is in the Web (DBpedia and / or Wikidata)

<h2>(1) DDSampling on local distributed databases</h2>

The main syntax is : <br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSamplingPAKDD20.jar <b>online:no</b> <b>sampleSize</b>:\<sample size\> <b>utility</b>:\<Freq or Area\> <b>dataset</b>:\<"connect" for example\> <b>maxLength</b>:\<maximal length constraint\> <b>pType</b>:\<partitioning type VL, HL, HD\> <b>nbSites</b>:\<number of sites\> <b>nbFailedSites</b>:\<number of failed sites\> <b>errorRate</b>:\<error rate\> <b>recordSample</b>:\<Yes or No for reccording the sampled patterns\> </i><br>


To enable you to evaluate DDSampling with the databases of the literature, we have made available the following bases in their partitioned forms as mentioned in the paper: "chess", "connect", "mushroom" and "waveform" which are in the <b> LocalDdistributedDataBases</b> folder.

	
********************************************************************************************************************************
	
\>java "-Dfile.encoding=UTF-8" -jar DDSamplingPAKDD20.jar online:no sampleSize:1000 utility:Freq dataset:connect maxLength:3 pType:VL nbSites:10 nbFailedSites:0 errorRate:0.0 recordSample:No

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

\>java "-Dfile.encoding=UTF-8" -jar DDSamplingPAKDD20.jar online:no sampleSize:1000 utility:Freq dataset:connect maxLength:3 pType:HL nbSites:10 nbFailedSites:0 errorRate:0.0 recordSample:Yes

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
	

\>java "-Dfile.encoding=UTF-8" -jar DDSamplingPAKDD20.jar online:no sampleSize:1000 utility:Area dataset:connect maxLength:3 pType:HD nbSites:10 nbFailedSites:0 errorRate:0.0 recordSample:Yes

	DDSampling on local distributed database : connect
	Running with parameters :
		Max length : 3
		Utility : Area
		Sample size : 1000
		Partition type : HD
	Preprocessing time (s) : 2.804
	Total number of instances : 67557
	Rejection rate : 0.0
	Please recover your sample from :
	OutputPatternsLocalDatabases/Area/HD/connect/connect1000N1m3M0z0_0p.TXT
	Sampling time (s) : 0.032
	*********** END ***************
	
	
********************************************************************************************************************************

<h2>(2) DDSampling on triplestores (DBpedia and Wikidata)</h2>

\> java "-Dfile.encoding=UTF-8" -jar DDSamplingPAKDD20.jar  <b>online:no</b> <b>sampleSize</b>:\<sample size\> <b>utility</b>:\<Freq or Area\> <b>dataset</b>:\<D, W or D+W (or DW)\> <b>maxLength</b>:\<maximal length constraint\> <b>class</b>:\<The class of DBpedia and Wikidata databases that one want to query\>

