1. srun --account lezh --mem 16g --pty bash
2. 创建一个txt文件：见leyi2
3. 复制到cmd
4. cat scripts/plink1
5. sbatch -A dsmwpred scripts/plink1 检查job提交情况
6. jobinfo 14135784 查看job info
7. squeue -u lezh 我名下的队伍


# 例子
[lezh@fe-open-01 zly]$ echo "#"'!'"/bin/bash
> #SBATCH --mem 15G
> #SBATCH -t 2:0:0
> #SBATCH -c 2
> #SBATCH --constraint \"s05\"
>
> ./software/plink --bfile ./ukbb_by_ancestry/data_qc --noweb --keep ./ukbb_by_ancestry/data_qc_1.fam --recode --make-bed --out ./ukbb_by_ancestry/data_region1
>
> “ > scripts/plink1
>
> ^C
[lezh@fe-open-01 zly]$ echo "#"'!'"/bin/bash
> #SBATCH --mem 15G
> #SBATCH -t 2:0:0
> #SBATCH -c 2
> #SBATCH --constraint \"s05\"
>
> ./software/plink --bfile ./ukbb_by_ancestry/data_qc --noweb --keep ./ukbb_by_ancestry/data_qc_1.fam --recode --make-bed --out ./ukbb_by_ancestry/data_region1
>
> " > scripts/plink1

[lezh@fe-open-01 zly]$
[lezh@fe-open-01 zly]$ cat scripts/plink1
#!/bin/bash
#SBATCH --mem 15G
#SBATCH -t 2:0:0
#SBATCH -c 2
#SBATCH --constraint "s05"

./software/plink --bfile ./ukbb_by_ancestry/data_qc --noweb --keep ./ukbb_by_ancestry/data_qc_1.fam --recode --make-bed --out ./ukbb_by_ancestry/data_region1


[lezh@fe-open-01 zly]$ sbatch -A dsmwpred scripts/plink1
Submitted batch job 14135784
[lezh@fe-open-01 zly]$ jobinfo 14135784

Name                : plink1
User                : lezh
Account             : dsmwpred
Partition           : short,normal
Nodes               : None assigned
Cores               : 2
GPUs                : 0
State               : PENDING (None)
ExitCode            : --
Submit              : 2023-02-23T14:23:30
Start               : --
End                 : --
Waited              : 00:00:16
Reserved walltime   : 02:00:00
Used walltime       : --
Used CPU time       : --
% User (Computation): --
% System (I/O)      : --
Mem reserved        : 15G
Max Mem used        : --
Max Disk Write      : --
Max Disk Read       : --
[lezh@fe-open-01 zly]$
[lezh@fe-open-01 zly]$ squeue -u lezh
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
          14135784 short,nor   plink1     lezh PD       0:00      1 (Priority)
[lezh@fe-open-01 zly]$