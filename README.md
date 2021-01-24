# ACM Research Coding Challenge (Spring 2021)

## No Collaboration Policy

**You may not collaborate with anyone on this challenge.** You _are_ allowed to use Internet documentation. If you _do_ use existing code (either from Github, Stack Overflow, or other sources), **please cite your sources in the README**.

## Submission Procedure

Please follow the below instructions on how to submit your answers.

1. Create a **public** fork of this repo and name it `ACM-Research-Coding-Challenge-S21`. To fork this repo, click the button on the top right and click the "Fork" button.
2. Clone the fork of the repo to your computer using `git clone [the URL of your clone]`. You may need to install Git for this (Google it).
3. Complete the Challenge based on the instructions below.
4. Submit your solution by filling out this [form](https://acmutd.typeform.com/to/uqAJNXUe).

## Question One

Genome analysis is the identification of genomic features such as gene expression or DNA sequences in an individual's genetic makeup. A genbank file (.gb) format contains information about an individual's DNA sequence. The following dataset in `Genome.gb` contains a complete genome sequence of Tomato Curly Stunt Virus. 

**With this file, create a circular genome map and output it as a JPG/PNG/JPEG format.** We're not looking for any complex maps, just be sure to highlight the features and their labels.

**You may use any programming language you feel most comfortable. We recommend Python because it is the easiest to implement. You're allowed to use any library you want to implement this**, just document which ones you used in this README file. Try to complete this as soon as possible.

Regardless if you can or cannot answer the question, provide a short explanation of how you got your solution or how you think it can be solved in your README.md file. However, we highly recommend giving the challenge a try, you just might learn something new!

## JADDYN'S SUMMARY

1. The first thing I did was look for libraries that could help in graphing a circular genome, because I am not willing to do all that work myself. I came across a few, but I      had trouble finding something that could fit the bill.

2. Then I came across this Java package called cgview.jar, created by Paul Stothard and David Wishart. I'll cite it below.
    
    Input requires specially-formatted files, of either .xml extension or.tab extension; in turn it spits out a circular genome.
    It would have been simpler to manually write a .tab file, given the small size of the viral genome, but I wanted to try the harder route.

3. In order to generate the .xml file for cgview.jar, you must run the Perl script cgview_xml_builder.pl, which is included in the project's GitHub.

4. I used Strawberry Perl's CPAN functionalities to download the modules needed to run the Perl script, but I ran into a problem: one of the modules did not download correctly, 
    due to some changes in Perl back in 2015. I tried tweaking the module's files, to no avail. Instead, I used a legacy version of Strawberry Perl (5.24.0.1), which in turn         comes with the legacy version of Perl I needed to download the module correctly.

5. After that, I could parse and extract the Genome.gb data into a test.xml file which, when run through cgview.jar, would generate a map.

6. But something didn't seem right -- all the genes were overlapping each other. I searched the Internet for a way to make the genes display separately, to no
    no avail. It seems that the creator of CGView did not account for overlapping genes!

    Instead, I had to tinker with the .xml file itself, manually wrapping gene in these <featureSlot> </featureSlot> things, also sprucing up the graph with colors and contrast     while I was at it. I don't know how XML works, but what matters is that I achieved my goal, right? It did render expediting the parsing process to the Perl script moot,         though. 

It took me a week to figure all of this out.

After I completed the challenge, I found http://cgview.ca/, which would have taken my Genome.gb file and spat out the map I wanted in under a minute.
But I don't think either of us would be satisfied with that, haha --

![## FINAL ANSWER:](https://raw.githubusercontent.com/Jad-Panjaitan/Coding-Challenge-S21/main/Final-Answer/finalanswer.png)

https://github.com/Jad-Panjaitan/Coding-Challenge-S21/blob/main/Final-Answer/finalanswer.png

## JADDYN'S POST-CHALLENGE REMARKS

1. Troubleshooting the map, figuring why such and such wasn't working or displaying correctly, was probably the toughest part of this challenge.
2. Fixing the broken Perl module and figuring out how terminals work was also pretty tough. But everything is easier in hindsight.
3. molbiol-tools.ca/Genomics.htm has a LOT of genome-related map stuff. So CGView isn't the only way to go about it.
4. I wonder how Aditya did it using Python on repl.it? Perhaps it would've been easier if I didn't decide to go the CGView route... 

## CITATIONS

CGView -- 
	Version -> 2.02, 2020-06-21
	APA Citation -> Stothard, P., & Wishart, D. S. (2005). Circular genome visualization and exploration using CGView. Bioinformatics (Oxford, England), 21(4), 537–539. 
	https://doi.org/10.1093/bioinformatics/bti054
	
	GitHub link -> https://github.com/paulstothard/cgview

Tie::IxHash module --
	Version -> 1.23
	Author -> Gurusamy Sarathy, gsar@umich.edu

Bio::SeqIO module --
	Version -> 1.7.7
	Author -> Ewan Birney, birney@ebi.ac.uk
	Author -> Lincoln Stein, lstein@cshl.org

Bio::SeqUtils module --
	Version -> 1.7.7
	Author -> Heikki Lehvaslaiho, heikki-at-bioperl-dot-org
	Contributors -> Roy R. Chaudhuri, roy.chaudhuri@gmail.com
	Contributors -> Frank Schwach, frank.schwach@sanger.ac.ul

## JADDYN'S WORK NOTES

I wonder if I should just take the codon datas and generate a plasmid map using that. 
That's the simple solution, but I want to see if I can make a program that takes in a GenBank file and spits out a circular genome map. Also why are these break lines so long? I need a mouse

Things we need?

	Locus name (the GenBank code for the virus): NC_004675
	Length: 2766 bp (base pairs)
	Features (information about genes and gene products): 
	ALSO include the loci!
	Source: bp 1 to bp 2766
		Organism Name: "Tomato blah blah blah"
		Molecule Type: genomic DNA
		Database crossreference: Taxon 128941
		Country: South Africa
	Gene: bp 139 to 480
		Gene: V2
		Locus tag: ToCSVgp1
		Database crossreference: 1460809
	CDS (coding sequences): bp 139 to 480
		Gene: same
		Locus tag: same
		Codon start: 1 (? what does that mean)
		Product: V2 Protein
		Protein ID: NP_8171151
		Database crossreference: same
		Translation (the actual amino acids that the base pairs code): MWDPLLNEFPDSVHGFRCMLAVKYLQSVEATYEPNTLGHDLIRD
                     LILVIRAKDYVEASRRYNHFHARLEGAEKAELRQPVHQPCCCPHCPRHKQATIMDVQA
                     HVSKAQDVQNV
	Gene: bp 299 to 1075 etc etc
	CDS: etc etc
	Gene: complement (1072.. 1476)
	CDS: complement (1072.. 1476)
	ETC more genes.. more CDS...

So what does "complement (bp range)" mean?

	(complement)  indicates that the feature is on the complementary strand

	Example:    complement(3300..4037)
	The feature extends from base 3300 through base 4037 but is actually on the complementary strand. 
	It is therefore read in the opposite direction on the reverse complement sequence. 
	In this case, the amino acid translation is generated by taking the reverse complement of bases 3300 to 4037 and reading that reverse complement sequence in its 5' to 3' direction

	ESSENTIALLY the arrow points other way.

What is GC Content, GC Skew +, GC Skew -?

	They all relate to the amount of Guanine-Cytosine bases in the frame. The skews are just a way to represent the relative amount of GC Content. Skews are interesting because they typically relate to leading and lagging strands.

Why aren't the labels showing?

	I need to specify to show gene and feature labels when I build the .xml file using that Perl script.

Why are all of the genes blending together?
	
	I don't know.

	UPDATE: I do know.
	I have to edit the .xml file I generated, and put each gene wrapped in <featureSlot> </featureSlot>. A bit troublesome, yes.

Why aren't the labels showing AGAIN?

	Because you were tinkering around with font size, you made the labels too large to display. The map is too small. Make it bigger.

	
