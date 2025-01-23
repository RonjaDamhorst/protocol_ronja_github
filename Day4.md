´´´bash
#path to contigs:
/work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/assembly_output5/contigs.db
#path to mapped_profiles:
/work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/mapped_profiles/PROFILE.db

#MAG quality estimation
anvi-estimate-genome-completeness -c /PATH/TO/contigs.db -p /PATH/TO/merged_profiles/PROFILE.db -C METABAT2
#used one 
anvi-estimate-genome-completeness -c /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/assembly_output5/contigs.db -p /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/mapped_profiles/PROFILE.db -C METABAT2


#then
anvi-estimate-genome-completeness -p /PATH/TO/merged_profiles/PROFILE.db -c /PATH/TO/contigs.db --list-collections
#used one
anvi-estimate-genome-completeness -p /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/mapped_profiles/PROFILE.db -c /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/assembly_output5/contigs.db --list-collections
#to display:
anvi-interactive -p /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/mapped_profiles/PROFILE.db -c /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/assembly_output5/contigs.db -C MAXBIN2


#bin refinment 
anvi-summarize -p ? -c ? --list-collections
anvi-summarize -c ? -p ? -C ? -o ? --just-do-it
#finish command 
anvi-summarize -p /PATH/TO/merged_profiles/PROFILE.db -c /PATH/TO/contigs.db --list-collections

anvi-summarize -c /PATH/TO/contigs.db -p /PATH/TO/merged_profiles/profile.db -C METABAT2 -o SUMMARY_METABAT2 --just-do-it
astp_output/4_mapping/SUMMARY_MAXBIN2/bin_by_bin/MAXBIN__011/*.fa /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/archeabin_refinment/

cd /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/SUMMARY_METABAT2/bin_by_bin
cp /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/SUMMARY_METABAT2/bin_by_bin/METABAT__8/*.fa /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/archeabin_refinment/

#Chimera detection MAGs 
#first activate env
module load gcc12-env/12.1.0
module load micromamba/1.3.1
micromamba activate 00_gunc
#then loop
cd /PATH/TO/ARCHAEA_BIN_REFINEMENT

for i in *.fa; do mkdir /PATH/TO/06_gunc/"$i"_out; done

for i in *.fa; do
  gunc run -i "$i" -r $WORK/databases/gunc/gunc_db_progenomes2.1.dmnd --out_dir /PATH/TO/06_gunc/"$i"_out --threads 8 --detailed_output
done
#used one:
cd /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/archeabin_refinment/
#before running the loop you need to 
mkdir 06_gunc
#and the underfolders for every bin in your archeabin_refinment like this:
mkdir MAXBIN_011-contigs.fa_out 
#then you can run the loop : 
for i in *.fa; do
  gunc run -i "$i" -r $WORK/databases/gunc/gunc_db_progenomes2.1.dmnd --out_dir /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/06_gunc/"$i"_out --threads 8 --detailed_output
done
# the next step for chimera detection:
cd /work_beegfs/sunam###/metagenomics/06_gunc/METABAT__###-contigs.fa_out
gunc plot -d ./diamond_output/METABAT__#-contigs.diamond.progenomes_2.1.out -g ./gene_calls/gene_counts.json
#replaye ### by number of archea MAG and do this for arch in a specific folder 
#used one :
#path to metbat:
/work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/06_gunc/ 
# for dimand do this for every single metbat folder in 06_gunc 
cd /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/06_gunc/MAXBIN__011-contigs.fa_out
gunc plot -d ./diamond_output/MAXBIN__011-contigs.diamond.progenomes_2.1.out -g ./gene_calls/gene_counts.json

#manual bin refinement
anvi-refine -c /PATH/TO/contigs.db -C METABAT -p /PATH/TO/merged_profiles/PROFILE.db --bin-id Bin_METABAT__##
#used command 
anvi-refine -c /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/assembly_output5/contigs.db -C METABAT -p /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/mapped_profiles/PROFILE.db  --bin-id Bin_METABAT__8

 #always use 
squeue -u sunam229
sbatch template.sh


#METBAT44 visualised:
```bash
```

![image](./resources/Bildschirmfoto%20vom%202025-01-23%2014-01-07.png)
![alt text](<resources/Bildschirmfoto vom 2025-01-23 14-10-53.png>)
![alt text](<resources/Bildschirmfoto vom 2025-01-23 14-11-42.png>)


