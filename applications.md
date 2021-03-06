### Software Usage on the Cluster

Objectives:
- Users can install software into their own directories, but there are other options for applications needed by multiple users.  Package manager software allows multiple users to utilize the same software installation while having it centrally managed by server administrators.
keypoints:

---
### Userspace Installation

In general, users are encouraged to install applications, scripts, modules and source code into directories under their control. For example:

~~~
/home/<userid>

/projects/<userid>
~~~

### Cluster-wide Installation (Research IT, helpdesk ticket required)

On Helix and Cadillac, common software is managed through the Enviornment Modules package.

To see what is installed, use the command `module -l avail`.

~~~
$ module -l avail
~~~

~~~
- Package -----------------------------+- Versions -+- Last mod. ------
/opt/software/helix/modulefiles:
454/default                                          2016/07/07 13:39:48
abacas/1.03                                          2016/04/05 15:01:20
abyss/1.9.0                                          2016/04/05 15:04:06
abyss/1.9.0-mpi                                      2016/07/28 15:00:24
act/13.0.0                                           2015/03/30 16:23:58
aga/0.1.0                                default     2016/08/24 16:24:17
aga/latest                                           2016/08/24 16:12:16
aga/test                                             2016/08/24 16:06:09
alamut/1.5.2                                         2016/09/14 16:14:14
alamut/1.5.2-standalone                              2016/10/14 18:15:59
alamut/1.5.2-test                                    2016/10/10 19:12:20
allpaths/52488                                       2016/04/18 13:35:44
amos/3.1.0                                           2015/11/25 15:03:53
Anaconda/2.4.0                                       2015/11/12 16:32:09
annovar/2014-11-12                                   2015/03/24 12:06:45
annovar/2015-03-22                                   2015/03/24 12:17:45
ant/1.9.4                                            2014/09/12 20:31:54
antismash/3.0                                        2016/08/05 13:51:40
apt/1.15.0                                           2015/08/12 19:00:15
armadillo/4.100.2                                    2014/04/01 15:35:07
artemis/13.0.0                                       2015/03/30 16:23:58
aspera/default                                       2015/12/23 13:04:29
BACH/070913                                          2014/04/01 22:22:29
bam-readcount/0                                      2014/11/28 17:14:08
bamtools/1.0.2                           default     2014/04/28 16:18:54
bamtools/2.3.0                                       2014/05/15 15:54:18
baysic/default                                       2015/10/19 15:28:00
bbmap/33.73                                          2014/11/06 18:01:45
bbmap/36.14                                          2016/07/07 19:10:59
...                                                  ...
ViennaRNA/2.1.7                                      2014/05/27 17:46:30
vim/7.4                                              2014/03/03 19:15:22
vim/7.4.1640                                         2016/03/23 20:25:40
vim/8.0                                              2016/12/05 22:46:01
WASP/default                                         2015/12/23 19:41:04
weblogo/2.8.2                                        2016/10/12 21:43:38
wgs/8.1                                              2014/03/04 13:28:11
wgs/8.3rc2                                           2015/06/25 17:03:54
xenome/1.0.0                                         2012/09/26 18:55:37
xlwt/0.7.4                                           2013/02/15 18:26:18
zsh/5.0.5                                            2014/03/03 19:32:18
~~~

To load a module, use the `module load [modulename/version]` command.

~~~
module load bowtie2/2.2.3
$ bowtie2 -h
~~~

~~~
Bowtie 2 version 2.2.3 by Ben Langmead (langmea@cs.jhu.edu, www.cs.jhu.edu/~langmea)
Usage:
  bowtie2 [options]* -x <bt2-idx> {-1 <m1> -2 <m2> | -U <r>} [-S <sam>]

  <bt2-idx>  Index filename prefix (minus trailing .X.bt2).
             NOTE: Bowtie 1 and Bowtie 2 indexes are not compatible.
  <m1>       Files with #1 mates, paired with files in <m2>.
             Could be gzip'ed (extension: .gz) or bzip2'ed (extension: .bz2).
  <m2>       Files with #2 mates, paired with files in <m1>.
             Could be gzip'ed (extension: .gz) or bzip2'ed (extension: .bz2).
  <r>        Files with unpaired reads.
             Could be gzip'ed (extension: .gz) or bzip2'ed (extension: .bz2).
  <sam>      File for SAM output (default: stdout)

  <m1>, <m2>, <r> can be comma-separated lists (no whitespace) and can be
  specified many times.  E.g. '-U file1.fq,file2.fq -U file3.fq'.

Options (defaults in parentheses):

 Input:
  -q                 query input files are FASTQ .fq/.fastq (default)
  --qseq             query input files are in Illumina's qseq format
  -f                 query input files are (multi-)FASTA .fa/.mfa
  -r                 query input files are raw one-sequence-per-line
  -c                 <m1>, <m2>, <r> are sequences themselves, not files
  -s/--skip <int>    skip the first <int> reads/pairs in the input (none)
  -u/--upto <int>    stop after first <int> reads/pairs (no limit)
  -5/--trim5 <int>   trim <int> bases from 5'/left end of reads (0)
  -3/--trim3 <int>   trim <int> bases from 3'/right end of reads (0)
  --phred33          qualities are Phred+33 (default)
  --phred64          qualities are Phred+64
  --int-quals        qualities encoded as space-delimited integers

 Presets:                 Same as:
  For --end-to-end:
   --very-fast            -D 5 -R 1 -N 0 -L 22 -i S,0,2.50
   --fast                 -D 10 -R 2 -N 0 -L 22 -i S,0,2.50
   --sensitive            -D 15 -R 2 -N 0 -L 22 -i S,1,1.15 (default)
   --very-sensitive       -D 20 -R 3 -N 0 -L 20 -i S,1,0.50

  For --local:
   --very-fast-local      -D 5 -R 1 -N 0 -L 25 -i S,1,2.00
   --fast-local           -D 10 -R 2 -N 0 -L 22 -i S,1,1.75
   --sensitive-local      -D 15 -R 2 -N 0 -L 20 -i S,1,0.75 (default)
   --very-sensitive-local -D 20 -R 3 -N 0 -L 20 -i S,1,0.50

 Alignment:
  -N <int>           max # mismatches in seed alignment; can be 0 or 1 (0)
  -L <int>           length of seed substrings; must be >3, <32 (22)
  -i <func>          interval between seed substrings w/r/t read len (S,1,1.15)
  --n-ceil <func>    func for max # non-A/C/G/Ts permitted in aln (L,0,0.15)
  --dpad <int>       include <int> extra ref chars on sides of DP table (15)
  --gbar <int>       disallow gaps within <int> nucs of read extremes (4)
  --ignore-quals     treat all quality values as 30 on Phred scale (off)
  --nofw             do not align forward (original) version of read (off)
  --norc             do not align reverse-complement version of read (off)
  --no-1mm-upfront   do not allow 1 mismatch alignments before attempting to
                     scan for the optimal seeded alignments
  --end-to-end       entire read must align; no clipping (on)
   OR
  --local            local alignment; ends might be soft clipped (off)

 Scoring:
  --ma <int>         match bonus (0 for --end-to-end, 2 for --local)
  --mp <int>         max penalty for mismatch; lower qual = lower penalty (6)
  --np <int>         penalty for non-A/C/G/Ts in read/ref (1)
  --rdg <int>,<int>  read gap open, extend penalties (5,3)
  --rfg <int>,<int>  reference gap open, extend penalties (5,3)
  --score-min <func> min acceptable alignment score w/r/t read length
                     (G,20,8 for local, L,-0.6,-0.6 for end-to-end)

 Reporting:
  (default)          look for multiple alignments, report best, with MAPQ
   OR
  -k <int>           report up to <int> alns per read; MAPQ not meaningful
   OR
  -a/--all           report all alignments; very slow, MAPQ not meaningful

 Effort:
  -D <int>           give up extending after <int> failed extends in a row (15)
  -R <int>           for reads w/ repetitive seeds, try <int> sets of seeds (2)

 Paired-end:
  -I/--minins <int>  minimum fragment length (0)
  -X/--maxins <int>  maximum fragment length (500)
  --fr/--rf/--ff     -1, -2 mates align fw/rev, rev/fw, fw/fw (--fr)
  --no-mixed         suppress unpaired alignments for paired reads
  --no-discordant    suppress discordant alignments for paired reads
  --no-dovetail      not concordant when mates extend past each other
  --no-contain       not concordant when one mate alignment contains other
  --no-overlap       not concordant when mates overlap at all

 Output:
  -t/--time          print wall-clock time taken by search phases
  --un <path>           write unpaired reads that didn't align to <path>
  --al <path>           write unpaired reads that aligned at least once to <path>
  --un-conc <path>      write pairs that didn't align concordantly to <path>
  --al-conc <path>      write pairs that aligned concordantly at least once to <path>
  (Note: for --un, --al, --un-conc, or --al-conc, add '-gz' to the option name, e.g.
  --un-gz <path>, to gzip compress output, or add '-bz2' to bzip2 compress output.)
  --quiet            print nothing to stderr except serious errors
  --met-file <path>  send metrics to file at <path> (off)
  --met-stderr       send metrics to stderr (off)
  --met <int>        report internal counters & metrics every <int> secs (1)
  --no-head          supppress header lines, i.e. lines starting with @
  --no-sq            supppress @SQ header lines
  --rg-id <text>     set read group id, reflected in @RG line and RG:Z: opt field
  --rg <text>        add <text> ("lab:value") to @RG line of SAM header.
                     Note: @RG line only printed when --rg-id is set.
  --omit-sec-seq     put '*' in SEQ and QUAL fields for secondary alignments.

 Performance:
  -p/--threads <int> number of alignment threads to launch (1)
  --reorder          force SAM output order to match order of input reads
  --mm               use memory-mapped I/O for index; many 'bowtie's can share

 Other:
  --qc-filter        filter out reads that are bad according to QSEQ filter
  --seed <int>       seed for random number generator (0)
  --non-deterministic seed rand. gen. arbitrarily instead of using read attributes
  --version          print version information and quit
  -h/--help          print this usage message
~~~

To see what module files you currently have loaded, use the `module list` command.

~~~
$ module list
~~~

~~~
Currently Loaded Modulefiles:
1) bowtie2/2.2.3
~~~

To unload a module, use the `module unload [modulename/version]` command.

~~~
$ module list
~~~

~~~
Currently Loaded Modulefiles:
  1) bowtie2/2.2.3
~~~

~~~
$ module unload bowtie2/2.2.3
$ module list
~~~

~~~
No Modulefiles Currently Loaded.
~~~

Applications installed as modules are located in `/opt/software/<cluster>`.  If you're unsure of a command, browse to `/opt/software/<cluster>` and look around to determine the proper command name.
