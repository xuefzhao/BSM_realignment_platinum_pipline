#build reference genome:
##commands we used to download the reference sequence and related files:
```
wget ftp://ftp-trace.ncbi.nih.gov/1000genomes/ftp/technical/reference/GRCh38_reference_genome/GRCh38_full_analysis_set_plus_decoy_hla.fa
wget ftp://ftp-trace.ncbi.nih.gov/1000genomes/ftp/technical/reference/GRCh38_reference_genome/README.20150309.GRCh38_full_analysis_set_plus_decoy_hla
```

###python script to exclude:Alternate loci scaffolds, Patch scaffolds and HLA sequences from the reference; 
```
#workdir: /nfs/turbo/dcmb-brainsom/technical/reference/GRCh38_bsm_reference_genome

import os
def chromosome_name_decide(chromo_name):
	if not '_' in chromo_name and not '-' in chromo_name: #canonical chromosomes
		return 'Include'
	else:
		if chromo_name.split('_')[-1] in ['random','decoy']:
			return 'Include'
		elif chromo_name.split('_')[0] =='>chrUn':
			return 'Include'
		elif chromo_name.split('_')[-1] in ['alt','patch']:
			print chromo_name
			return 'Exclude'
		elif chromo_name.split('-')[0]=='>HLA':
			print chromo_name
			return 'Exclude'
		else:
			print 'Situation not considered:'
			print chromo_name
			return ''
filein='GRCh38_full_analysis_set_plus_decoy_hla.fa'
fileout_keep='GRCh38_BSM_analysis_V1.fa'
fileout_else='GRCh38_BSM_analysis_V1_excluded.fa'
fin=open(filein)
fo1=open(fileout_keep,'w')
fo2=open(fileout_else,'w')
keep_status=''
for line in fin:
	pin=line.strip().split()
	if pin[0][0]=='>':
		print pin
		keep_status=chromosome_name_decide(pin[0])
	if keep_status=='Include':
		print >>fo1, '  '.join(pin)
	elif keep_status=='Exclude':
		print >>fo2, '  '.join(pin)
	else:
		break
fin.close()
fo1.close()
fo2.close()
```

##commands we used to download and install each tool:
###samtools:
```
wget https://github.com/samtools/samtools/releases/download/1.3/samtools-1.3.tar.bz2 
bunzip2 samtools-1.3.tar.bz2
tar -xvf samtools-1.3.tar 
./configure --prefix=/nfs/remills-data/local/bin/
make
make install
```

###bwa:
```
wget http://sourceforge.net/projects/bio-bwa/files/bwakit/bwakit-0.7.12_x64-linux.tar.bz2/download
mv download bwakit-0.7.12_x64-linux.tar.bz2
bunzip2 bwakit-0.7.12_x64-linux.tar.bz2 
tar -xvf bwakit-0.7.12_x64-linux.tar 
mv bwa.kit/ bwa-0.7.12
```

###blasr
```
git clone https://github.com/EichlerLab/blasr.git
make
```


##commands we used to index reference:
###samtools index:
```
/nfs/turbo/dcmb-brainsom/technical/application/samtools-1.3/samtools faidx /nfs/turbo/dcmb-brainsom/technical/reference/GRCh38_bsm_reference_genome/GRCh38_BSM.fa
```

###bwa index:
```
/nfs/turbo/dcmb-brainsom/technical/application/bwa-0.7.12/bwa index /nfs/turbo/dcmb-brainsom/technical/reference/GRCh38_bsm_reference_genome/GRCh38_BSM.fa
```

###blasr index
```
sawriter hg19.fasta.sa hg19.fasta
/nfs/turbo/dcmb-brainsom/technical/application/blasr/alignment/bin/sawriter /nfs/turbo/dcmb-brainsom/technical/reference/GRCh38_bsm_reference_genome/GRCh38_BSM.blasr.sa /nfs/turbo/dcmb-brainsom/technical/reference/GRCh38_bsm_reference_genome/GRCh38_BSM.fa
```

