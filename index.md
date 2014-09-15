## TGAC - AllBio 2014

<!-- We will need a Flash presentation from you which should be a maximum of 5 minutes with a brief introduction and synopsis of your career plus your work/involvement in the areas this workshop is covering and a maximum of 4 slides - this needs to be with us by latest 8 September (apologies for the short notice). -->

<small style="float: right;"><a href="//bmpvieira.com/allbio14" target="_blank">bmpvieira.com/allbio14</a></small>
<br>

<img style="width: 30%; float: right; padding-right: 1em;" alt="bmpvieira" src="img/bmpvieira.png" />

[Bruno Vieira](http://bmpvieira.com) | <i class="fa fa-twitter"></i> <a href="//twitter.com/bmpvieira" target="_blank">@bmpvieira</a>

Phd Student @ <a href="http://www.qmul.ac.uk" target="_blank"><img style="width: 25%; float: right; padding-right: 1em;" alt="QMUL" src="img/Queen_Mary,_University_of_London_logo.svg" /></a>

Bioinformatics and Population Genomics

<span style="font-size:0.8em;">
Supervisor:  
Yannick Wurm | <i class="fa fa-twitter"></i>  <a href="//twitter.com/yannick__" target="_blank">@yannick__</a>
</span><br>
<small>
Before:
<br>
<a href="http://www.ciencias.ulisboa.pt" target="_blank"><img style="max-height: 7%;  float: left;" alt="FCUL" src="img/fcul.png" /></a>
<a href="http://cobig2.com" target="_blank"><img style="max-height: 7%; float: left;" alt="CoBiG2" src="img/cobig2.png" /></a>
<a href="http://eseb2013.com" target="_blank"><img style="max-height: 7%; float: left;" alt="eseb2013" src="img/eseb2013.png" /></a>
<a href="https://geekli.st" target="_blank"><img style="max-height: 7%; float: left;" alt="geeklist" src="img/geeklist.png" />
<a href="http://www.bbsrc.ac.uk" target="_blank"><img style="max-height: 7%; float: left;" alt="bbsrc" src="img/bbsrc.png" />

</small>
<div style="position:absolute; top: 82%; font-size:.35em;">
© 2014 <a href="http://bmpvieira.com" target="_blank">Bruno Vieira</a> <a href="http://creativecommons.org/licenses/by/4.0/deed.en_US" target="_blank">CC-BY 4.0</a>
</div>


---

### Some problems I faced during my research:

* Difficulty getting relevant descriptions and datasets from NCBI API using bio\* libs  
<!-- **Solution**: Write a more user friendly and Streamable library/CLI tool -->

* For web projects, needed to implement the same functionality on browser and server
<!-- **Solution**: JavaScript everywhere -->

* Difficulty writing scalable, reproducible and complex bioinformatic pipelines
<!-- **Solution**: Streams everywhere -->

---

<!-- <div style="float: left; max-width:10%"> -->

**[Bionode.io](http://bionode.io)** - <span style="font-size: .8em;">*Modular and universal bioinformatics*</span>
<img style="width: 20%;float: right; padding-right: 1em;" alt="bionode" src="img/bionode-logo.svg" />

<span style="font-size: .7em; line-height:10%;">Pipeable UNIX command line tools and JavaScript / Node.js APIs for bioinformatic analysis workflows on the server and browser.<br><span style="font-size:.7em;">Collaborates with [BioJS](http://biojs.net/) - *Represent biological data on the web*</span></span>

<div style="padding-bottom:2em;"></div>

<img style="width: 17%;float: left; padding-right: .5em;" alt="dat" src="img/dat.png" />
**[Dat](http://dat-data.com) ** - <span style="font-size: .8em;">*Build data pipelines*</span>

<span style="font-size: .7em; line-height:10%;">Provides a streaming interface between every file format and data storage backend. *"git for data"*</span>

<small>[dat-data.com](http://dat-data.com)
| <i class="fa fa-twitter"></i> [@maxogden](https://twitter.com/@maxogden)
| <i class="fa fa-twitter"></i> [@mafintosh](https://twitter.com/@mafintosh)
</small>

---

<span style="font-size:3.0em;">
[bionode.io](http://bionode.io)
</span>[(online shell)](http://try.bionode.io)

**Examples**

BASH

<pre>
 bionode-ncbi urls assembly Solenopsis invicta | grep genomic.fna

 <a href="http://ftp.ncbi.nlm.nih.gov/genomes/all/GCA_000188075.1_Si_gnG/GCA_000188075.1_Si_gnG_genomic.fna.gz" >http://ftp.ncbi.nlm.nih.gov/genomes/all/GCA_000188075.1_Si_gnG/
 GCA_000188075.1_Si_gnG_genomic.fna.gz</a>
</pre>

<pre>
 bionode-ncbi download sra arthropoda | bionode-sra
</pre>

<pre>
 bionode-ncbi download gff bacteria
</pre>

JavaScript
```javascript
var ncbi = require('bionode-ncbi')
 ncbi.urls('assembly', 'Solenopsis invicta'), gotData)
 function gotData(urls) {
   var genome = urls[0].genomic.fna
   download(genome)
 })
```
```bash
ncbi.search('biosample', 'human').pipe(filter).pipe(analyse)
```

---

** Difficulty getting relevant description and datasets from NCBI API using bio* libs **

Python example

```python
import xml.etree.ElementTree as ET
 from Bio import Entrez
 Entrez.email = "mail@bmpvieira.com"
 esearch_handle = Entrez.esearch(db="assembly", term="Achromyrmex")
 esearch_record = Entrez.read(esearch_handle)
 for id in esearch_record['IdList']:
   esummary_handle = Entrez.esummary(db="assembly", id=id)
   esummary_record = Entrez.read(esummary_handle)
   documentSummarySet = esummary_record['DocumentSummarySet']
   document = documentSummarySet['DocumentSummary'][0]
   metadata_XML = document['Meta'].encode('utf-8')
   metadata = ET.fromstring('<root>' + metadata_XML + '</root>')
   for entry in Metadata[1]:
     print entry.text
```
<a href="ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA_000188075.1_Si_gnG"><pre>ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA_000188075.1_Si_gnG</pre></a>

Solution: <a href="http://github.com/bionode/bionode-ncbi">bionode-ncbi</a>

---


** Need to reimplement the same code on browser and server. **

Solution: JavaScript everywhere

* Afra
* SequenceServer
* GeneValidator
* BioJS

<br>
Biodalliance is converting parsers to Bionode

---

**Difficulty writing scalable, reproducible and complex bioinformatic pipelines.**

Solution: Node.js Streams everywhere

<pre>
 var ncbi = require('bionode-ncbi')
 var tool = require('tool-stream')
 var through = require('through2')
 var fork1 = through.obj()
 var fork2 = through.obj()

 ncbi
   .search('sra', 'Solenopsis invicta')
   .pipe(fork1)
   .pipe(dat.reads)

 fork1
   .pipe(tool.extractProperty('expxml.Biosample.id'))
   .pipe(ncbi.search('biosample'))
   .pipe(dat.samples)

 fork1
   .pipe(tool.extractProperty('uid'))
   .pipe(ncbi.link('sra', 'pubmed'))
   .pipe(ncbi.search('pubmed'))
   .pipe(dat.papers)
</pre>

---

### Benefit from other JS projects

<div style="float: left; padding-right:2em; width:20%;">
<a href="http://dat-data.com" target="_blank">Dat</a>
<img style="width:100%;" alt="dat" src="img/dat.png" />
</div>

<div style="float: left; padding-right:2em; width:20%;">
<a href="http://biojs.net" target="_blank">BioJS</a>
<img style="width:100%;" alt="biojs" src="img/biojs.png" />
</div>

<div style="float: left; padding-right:2em; width:20%;">
<a href="http://noflojs.org" target="_blank">NoFlo</a>
<img style="width:100%;" alt="noflo" src="img/noflo.jpg" />
</div>

---

<section data-background="img/noflo.png"></section>

---

<!--
<img style="float: left; padding-right:.5em; width:100%;" alt="streams" src="img/streams2.gif" />


--- -->

<section data-background="img/dat-table.png"></section>

---

### Reusable, small and tested modules

![badges](img/badges.png)

---

Users and Contributors:
* [Dat](htpp://dat-data.com)
* [Biodalliance](http://biodalliance.org)
* [BioJS](http://biojs.net)
* [Yeo Lab](http://yeolab.ucsd.edu/yeolab/Home.html) (UC San Diego)
  * Michael Lovci
  * Olga Botvinnik
* [Afra](http://afra.sbcs.qmul.ac.uk)
* [GeneValidator](github.com/monicadragan/GeneValidator))

Soon?
* [DNADigest](http://dnadigest.org)
* Erik Garrison | <i class="fa fa-twitter"></i> [erikgarrison](https://twitter.com/erikgarrison)


<!-- <br>
** Get all FASTQ for a specific accession **
```bash
bionode-ncbi download sra ERP003956 | bionode-sra
``` -->

---

<!-- <section data-background="img/bionode-graph.png"></section>

---

<section data-background="img/dat-graph.png"></section>

--- -->

<!-- ### CommonJS pattern

```javascript
// awesome-lib/index.js
module.exports = function() {
  return console.log("Small modules everywhere")
}

// myscript.js
var awesome = require('awesome-lib')
awesome()
``` -->


<!-- ### Command Line Interface

```bash

# Subset a fasta file to a particular sequence

cat sequences.fasta
| bionode-fasta
| grep "contig123"
| bionode-fasta --write > contig123.fasta


# Find the reads datasets used for the Solenopsis invicta assembly

bionode-ncbi search assembly Solenopsis invicta |
tool-stream extractProperty uid                 |
bionode-ncbi link assembly bioproject           |
tool-stream extractProperty destUID             |
bionode-ncbi link bioproject sra                |
tool-stream extractProperty destUID             |
bionode-ncbi urls sra                           |
dat import --json

```

--- -->

<!-- ### Project status: available

* Data access:
  * ncbi
* Parsing
  * fasta
  * bbi
* Wrangling
  * seq
* Wrappers
  * sra
  * sam
  * bwa

---

### Project status: down the line

<div style="font-size: .8em; line-height: 1.2em;">
<ul>
<li> Data access:
  <ul>
  <li> ebi </li>
  <li> ensembl </li>
  </ul>
<li> Parsing </li>
  <ul>
  <li> fastq </li>
  <li> sam </li>
  <li> vcf </li>
  <li> gff </li>
  </ul>
<li> Wrangling </li>
  <ul>
  <li> quality control/stats </li>
  </ul>
<li> Wrappers </li>
  <ul>
  <li> blast </li>
  <li> diginorm </li>
  </ul>
</ul>
</div>

--- -->

<!-- ### Try



### Install

#### Node

```bash
# OSX
brew install node
```

```bash
# Ubuntu
sudo apt-get install nodejs npm
```

#### Bionode

```bash
npm install bionode
```

--- -->

### Thanks!

Acknowledgements:

<i class="fa fa-twitter"></i> [@yannick__](http://twitter.com/yannick__)  
<i class="fa fa-twitter"></i> [@maxogden](http://twitter.com/maxogden)  
<i class="fa fa-twitter"></i> [@mafintosh](https://twitter.com/mafintosh)  
<i class="fa fa-twitter"></i> [@alanmrice](http://twitter.com/alanmrice)  
<i class="fa fa-twitter"></i> [@dasmoth](http://twitter.com/dasmoth)

---

### Why Node.js / JavaScript

* [Streams](http://nodejs.org/api/stream.html) applies well to Bioinformatics
* Easy to write [CLI wrappers](https://github.com/bionode/bionode-ncbi#command-line-examples) for Streams
* [Reusable, small and tested modules](https://github.com/bionode/bionode-ncbi#bionode-ncbi)
* Same language everywhere (JavaScript)
* Package Manager that works ([NPM](http://npmjs.org))
* Huge number modules ([93327, 199/day](http://www.modulecounts.com))
* Use other JS projects ([Dat](http://dat-data.com), [BioJS](http://biojs.net), [NoFlo](http://noflojs.org))
* Possible to write [Desktop GUI apps in JS](https://github.com/atom/atom-shell#atom-shell-)

---

### Module counts

<img style="width:80%;" alt="modules" src="img/modules.png" />

---

Package Manager that works

<img style="width: 25%;" alt="NPM" src="img/npm.png"/>

```bash

npm install bionode
npm install bionode -g
npm test
npm start
npm run test-browser
npm run build-docs
npm init
npm publish

```
