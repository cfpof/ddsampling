<h1>Patterns Sampling in Distributed Databases</h1>

						*ADBIS'2020

To run <b>DDSampling.jar</b>, we want to unzip the DDSampling.zip file and put the jar file into this folder. Into the DDSampling folder there are 4 sub-folders. In the <b>InputMatrix</b> folder, we have the weight matrix (<b>matPond_C</b>, where <b>C</b> is the class) that we used to sample pattern from the distributed database (<b>DBpedia+Wikidata</b>). The files "matPond_Organisation.zip", "matPond_Person.zip" and "matPond_matPond_RaceTrack.TXT" are some examples that we used. If you want to use one of them, just copy it in the InputMatrix folder. The folder <b>LocalDistributedDatabases</b> contains the UCI databases partitioned horizontally (HL), vertically (VL) and finally in a hybrid manner (HD). The two other <b>Output*</b> folders contain the sampled pattern respectively from  UCI local datasets and Triplestore databases. The UCI datasets allow us to do local simulations such as site failures, non stability of the internet connection, etc. <br>
In addition, DDSampling can take into account utility measures such as the frequency (Freq) or the area (Area) of a pattern.

Now with the command line, move into the DDSampling folder (<i>DDSampling/</i>) and run one of the following requests.<br> In our experiments, we distinguished two cases: 

	(1) The database is distributed but stored locally. 
	(2) The database is in the Web (DBpedia and / or Wikidata)

<h2>(1) DDSampling on local distributed databases</h2>

The main syntax is : <br>
	<i>\>java "-Dfile.encoding=UTF-8" -jar DDSampling.jar <b>online:no</b> <b>sampleSize</b>:\<sample size\> <b>utility</b>:\<Freq or Area\> <b>dataset</b>:\<"connect" for example\> <b>maxLength</b>:\<maximal length constraint\> <b>pType</b>:\<partitioning type VL, HL, HD\> <b>nbSites</b>:\<number of sites\> <b>nbFailedSites</b>:\<number of failed sites\> <b>errorRate</b>:\<error rate\> <b>recordSample</b>:\<Yes or No for reccording the sampled patterns\> </i><br>


To enable you to evaluate DDSampling with the databases of the literature, we have made available the following bases in their partitioned forms as mentioned in the paper: "chess", "connect", "mushroom" and "waveform" which are in the <b> LocalDdistributedDataBases</b> folder.

	
********************************************************************************************************************************
	
\>java "-Dfile.encoding=UTF-8" -jar DDSampling.jar online:no sampleSize:1000 utility:Freq dataset:connect maxLength:3 pType:VL nbSites:10 nbFailedSites:0 errorRate:0.0 recordSample:No

	DDSampling on local distributed database : connect
	Running with parameters :
		Max length : 3
		Utility : Freq
		Sample size : 1000
		Partition type : VL
	Preprocessing time (s) : 2.883
	Total number of instances : 67557
	Rejection rate : 0.0
	Sampling time (s) : 0.019
	*********** END ***************

\>java "-Dfile.encoding=UTF-8" -jar DDSampling.jar online:no sampleSize:1000 utility:Freq dataset:connect maxLength:3 pType:HL nbSites:10 nbFailedSites:0 errorRate:0.0 recordSample:Yes

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
	

\>java "-Dfile.encoding=UTF-8" -jar DDSampling.jar online:no sampleSize:1000 utility:Area dataset:connect maxLength:3 pType:HD nbSites:10 nbFailedSites:0 errorRate:0.0 recordSample:Yes

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

The main syntax is : <br>
<i>\> java "-Dfile.encoding=UTF-8" -jar DDSampling.jar  <b>online:yes</b> <b>sampleSize</b>:\<sample size\> <b>utility</b>:\<Freq or Area\> <b>dataset</b>:\<D, W or D+W (or DW)\> <b>maxLength</b>:\<maximal length constraint\> <b>class</b>:\<The class of DBpedia and Wikidata databases that one want to query\></i><br>
	
Here are some Web databases describing classes with joint properties to DBpedia and Wikidata :

	Book	RaceTrack	MusicalArtist	Scientist	Royalty	Song	Actor	Writer
	Language	Genre	Food	Station	TimePeriod	Cartoon	Case	Race	Biomolecule
	Judge	ChemicalSubstance	SportFacility	Plant	MotorsportRacer	SportsTeamSeason
	SportsManager	Cleric	Animal	FictionalCharacter	Politician	SocietalEvent	Event
	Infrastructure	Stream	PeriodicalLiterature	SportsTeam	Software	BodyOfWater	Group
	Broadcaster	NaturalPlace	WrittenWork	Artist	EducationalInstitution	Building	MusicalWork
	Company	ArchitecturalStructure	Athlete	Work	Settlement	PopulatedPlace	Organisation	Place	Person
	
During the experiments, we found that the construction phase of the weight matrix is very expensive with large databases because it requires a good internet connection. To show you the difference, we have also distinguished two cases:

	(a) Pretreatment with online matrix construction.
	(a) Pretreatment from the weight matrix already built and stored locally.
	
	
<h3>(a) with the class "RaceTrack"</h3>
	
\>java "-Dfile.encoding=UTF-8" -jar DDSampling.jar online:yes sampleSize:1000 utility:Freq dataset:DW maxLength:3 class:RaceTrack
	
	DDSapmling on RaceTrack data ...
	Running with parameters :
		Class : RaceTrack
		Utility : Freq
		Sample size : 1000
		Datasets : DW
		Max length : 3
	10000
	20000
	Preprocessing time (s) : 3.155
	Total number of entities : 400
	Please recover your sample from :
	OutputRDFpatterns/DBpedia_RaceTrack_M3N1000.TXT
	Sampling time (s) : 317.742
	Cost of communication for sampling : 2960.0±0.0
	Rejetion rate : 0.0±0.0
	*********** END ***************

<h3>(b) with the class "RaceTrack"</h3>

\>java "-Dfile.encoding=UTF-8" -jar DDSampling.jar online:yes sampleSize:1000 utility:Freq dataset:DW maxLength:3 class:RaceTrack
	
	DDSapmling on RaceTrack data ...
	Running with parameters :
		Class : RaceTrack
		Utility : Freq
		Sample size : 1000
		Datasets : DW
		Max length : 3
	Preprocessing time (s) : 0.048
	Total number of entities : 400
	Please recover your sample from :
	OutputRDFpatterns/DBpedia_RaceTrack_M3N1000.TXT
	Sampling time (s) : 552.659
	Cost of communication for sampling : 2957.0±0.0
	Rejetion rate : 0.0±0.0
	*********** END ***************

<h3>(a) with the class "Organisation"</h3>

\>java "-Dfile.encoding=UTF-8" -jar DDSampling.jar online:yes sampleSize:1000 utility:Freq dataset:DW maxLength:3 class:Organisation

	DDSapmling on Organisation data ...
	Running with parameters :
		Class : Organisation
		Utility : Freq
		Sample size : 1000
		Datasets : DW
		Max length : 3
	10000
	20000
	...
	340000
	350000
	Preprocessing time (s) : 2024.448
	Total number of entities : 338402
	Please recover your sample from :
	OutputRDFpatterns/DBpedia_Organisation_M3N1000.TXT
	Sampling time (s) : 379.48
	Cost of communication for sampling : 2960.0±0.0
	Rejetion rate : 0.0±0.0
	*********** END ***************

<h3>(b) with the class "Organisation"</h3>

\>java "-Dfile.encoding=UTF-8" -jar DDSampling.jar online:yes sampleSize:1000 utility:Freq dataset:DW maxLength:3 class:Organisation
	
	DDSapmling on Organisation data ...
	Running with parameters :
		Class : Organisation
		Utility : Freq
		Sample size : 1000
		Datasets : DW
		Max length : 3
	Preprocessing time (s) : 1.861
	Total number of entities : 338402
	Please recover your sample from :
	OutputRDFpatterns/DBpedia_Organisation_M3N1000.TXT
	Sampling time (s) : 343.528
	Cost of communication for sampling : 2958.0±0.0
	Rejetion rate : 0.0±0.0
	*********** END ***************

As the results show, when we run these experiments, the error rate is 0 because the bases are accessible, the connection is stable, and the weight matrix has just been created. However, we also noticed that with weight matrices stored locally for a few weeks, rejection rates are not zero, even if they remain low. This phenomenon is due to the fact that triplestores are updated frequently. <b>Another reason for not centralizing Web databases is that centralized information is not always identical to that available on the Web after a week</b>. Therefore, if you get non-zero error rates when testing with Web databases while the connection is stable, simply delete the locally stored weight matrix, and then restart the DDSampling algorithm.
