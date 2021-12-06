# fast_sampen_impl: Implementation for Fast Sample Entropy Computation
## Requirements
- OS: Linux or macOS;
- GSL should be installed.

## Usage
```text
Usage: fast_sampen --input <INPUT> --input-type {simple, multirecord}\
                   -r <THRESHOLD> -m <TEMPLATE_LENGTH>\
                   -n <N> [-output-level {1,2,3}]\
                   --sample-size <SAMPLE_SIZE> --sample-num <SAMPLE_NUM>

Arguments:
--input <INPUT>         The file name of the input file.
--input-format <FORMAT> The format of the input file. Should be either 'simple'
                        or 'multirecord'. If set to simple, then each line of the
                        input file contains exactly one column; if set to
                        multirecord, then each line contains <NUM_RECORD> + 1
                        columns, of which the first indicates the line number
                        and the remaining columns are instances of the records.
                        The default value is simple.
--input-type <TYPE>     The data type of the input data, either int or float.
                        Default: double.
-r <R>                  The threshold argument in sample entropy.
-m <M>                  The template length argument of sample entropy. Note
                        that this program only supports 2 <= m <= 10.
-n <N>                  If the length of the signal specified by <FILENAME> is
                        greater than <N>, then it would be truncated to be of
                        length <N>. If <N> is 0, then the the original length
                        is employed. The default value is 0.
--sample-size <N0>      The number of points to sample.
--sample-num <N1>       The number of computations where the average is taken.
--output-level <LEVEL>  The amount of information printed. Should be one of
                        {0,1,2}. Level 0 is most silent while level 2 is for
                        debugging.
--quasi-type <TYPE>     The type of the quasi-random sequence for sampling,
                        can be one of the following: sobol, halton,
                        reversehalton or niederreiter_2. Default: sobol.

Options:
-d | --direct           If this option is on, then (plain) direct method will be
                        conducted.
-fd | --fast-direct     If this option is on, then fast direct method will be
                        conducted.
--random                If this option is enabled, the random seed will be set
                        randomly.
-q                      If this option is enabled, the quasi-Monte Carlo based
                        method is conducted.
--variance              If this option is enabled, then the variance of the
                        results of sampling methods will be computed.
--n-computation <NC>    The number of computations for variance computation
                        (defualt = 50).
-u | --uniform          If this option is enabled, the Monte Carlo based
                        method using uniform distribution will be conducted.
--swr                   If this option is enabled, then the Monte Carlo based
                        method without placement will be performed.
--grid                  If this option is enabled, then the quasi-Monte Carlo
                        based method using grid (lattice) as sampling indexes
                        will be performed.
--presort               If this option is enabled, then a presorting operation
                        is conducted before sampling in quasi-Monte Carlo
                        based method.
```
