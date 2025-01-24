# day-5 protocol
## 20-01-2025


```bash
# go to work 
cd /work_beegfs/sunam###/metagenomics
#then activate env
module load gcc12-env/12.1.0
module load micromamba/1.3.1
micromamba activate 00_anvio

#taxonimic assignment 
anvi-run-scg-taxonomy -c /PATH/TO/contigs.db -T 20 -P 2
#used one 
anvi-run-scg-taxonomy -c /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/assembly_output5/contigs.db -T 20 -P 2
#dann:
squeue -u sunam229
sbatch template.sh
# then do the next command :
anvi-estimate-scg-taxonomy -c /PATH/TO/contigs.db -p /PATH/TO/profile.db --metagenome-mode --compute-scg-coverages --update-profile-db-with-taxonomy > temp.txt
#used one 
anvi-estimate-scg-taxonomy -c /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/assembly_output5/contigs.db -p /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/mapped_profiles/PROFILE.db --metagenome-mode --compute-scg-coverages --update-profile-db-with-taxonomy > temp.txt
#then do the next one:
anvi-summarize -p /PATH/TO/merged_profiles/PROFILE.db -c /PATH/TO/contigs.db -o /PATH/TO/SUMMARY_METABAT2 -C METABAT2
#used one 
anvi-summarize -p /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/mapped_profiles/PROFILE.db -c /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/assembly_output5/contigs.db -o /work_beegfs/sunam229/metagenomics/0_raw_reads/fastp_output/4_mapping/SUMMARY_METABAT2/final_summary -C METABAT2
# results:
#methanoculleus sp012797575
#does the HQ assihment of the bin need revision? -> you could lower the red. 












