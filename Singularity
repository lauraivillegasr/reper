Bootstrap:docker
From:ubuntu:latest

%labels
MAINTAINER nterhoeven

%environment
reperDir=/reper
export reperDir

depDir=/dependencies
export depDir

PATH=$reperDir:$PATH
export PATH

PERL5LIB=$depDir/lib:$PERL5LIB
export PERL5LIB

TRINITY_HOME=$depDir/trinityrnaseq-Trinity-v2.4.0
export TRINITY_HOME

%post
apt-get update && apt-get install -y  dist-upgrade && apt-get -y install wget g++ build-essential unzip libncurses5-dev zlib1g-dev libbz2-dev liblzma-dev libtbb-dev git libipc-run-perl python emacs openjdk-8-jre icedtea-8-plugin bc

cd $depDir


wget https://github.com/gmarcais/Jellyfish/releases/download/v2.2.6/jellyfish-2.2.6.tar.gz && tar xzf jellyfish-2.2.6.tar.gz && cd jellyfish-2.2.6 && ./configure && make && make install
wget https://github.com/trinityrnaseq/trinityrnaseq/archive/Trinity-v2.4.0.tar.gz && tar xzf Trinity-v2.4.0.tar.gz && cd trinityrnaseq-Trinity-v2.4.0 && make && make plugins
wget https://github.com/weizhongli/cdhit/releases/download/V4.6.7/cd-hit-v4.6.7-2017-0501-Linux-binary.tar.gz && tar xzf cd-hit-v4.6.7-2017-0501-Linux-binary.tar.gz
wget https://github.com/BenLangmead/bowtie2/releases/download/v2.3.2/bowtie2-2.3.2-linux-x86_64.zip && unzip bowtie2-2.3.2-linux-x86_64.zip
wget https://github.com/samtools/samtools/releases/download/1.4.1/samtools-1.4.1.tar.bz2 && tar xjf samtools-1.4.1.tar.bz2 && cd samtools-1.4.1 && ./configure && make && make install
wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/2.2.28/ncbi-blast-2.2.28+-x64-linux.tar.gz && tar xzf ncbi-blast-2.2.28+-x64-linux.tar.gz
git clone https://github.com/thackl/kmer-scripts.git

cd $depDir/lib
wget http://search.cpan.org/CPAN/authors/id/M/MS/MSCHILLI/Log-Log4perl-1.49.tar.gz && tar xzf Log-Log4perl-1.49.tar.gz && cd Log-Log4perl-1.49 && perl Makefile.PL && make && make install
git clone https://github.com/BioInf-Wuerzburg/perl5lib-Fastq.git && mv perl5lib-Fastq/lib/* .
git clone https://github.com/BioInf-Wuerzburg/perl5lib-Fasta.git && mv perl5lib-Fasta/lib/* .
git clone https://github.com/thackl/perl5lib-Jellyfish.git && mv perl5lib-Jellyfish/lib/* .
wget http://search.cpan.org/CPAN/authors/id/P/PL/PLICEASE/File-Which-1.22.tar.gz && tar xzf File-Which-1.22.tar.gz && cd File-Which-1.22 && perl Makefile.PL && make && make install
git clone https://github.com/thackl/perl5lib-Kmer.git && mv perl5lib-Kmer/lib/* .
git clone https://github.com/BioInf-Wuerzburg/perl5lib-Verbose.git && mv perl5lib-Verbose/lib/* .
git clone https://github.com/thackl/perl5lib-Sam.git && mv perl5lib-Sam/lib/* .

cd $reperDir
chmod -R ga+rwX $reperDir
chmod -R ga+rwX $depDir

%runscript
reper