# ns3-testing

Official repository at:
https://github.com/teto/ns3-testing

This repository hosts wrappers around the ns3 testing system in order to ease some common operations.

For instance, it can load specific command line arguments if the chosen test supports extra arguments.
This way tests can run extra scripts before running or other scripts to postprocess the data.
Tests should also not be automatically run. You may want to only postprocess the data generated by the script.

For instance, the mptcp-tcp test will:
1. Empty statistics folders
2. Run
3. Generate plots based on the newly saved statistics

Helper scripts to help debug ns3 applications (wrappers)


# How to use ?
You need to setup in test_ns3.py the variables:
- ns3folder
- dcefolder

And that's all !
The script relies on python's argparse library and as such should be self documented.

Here is an example on how to launch an 'example' (replace by 'test' for a 'test')
$ ./test_ns3.py example dce-iperf-mptcp-mixed --clean --load-log=ns_log.txt

or a more complex example for DCE mixing stacks:
$ ~/ns3testing/test_ns3.py example dce-iperf-mptcp-mixed --clean --load-log=ns_log.txt --out=xp.log --nRtrs=1 --debug --ChecksumEnabled=1 --clientStack=linux --serverStack=linux

For the ns_log.txt format, look at the one in this repository



MPTCP tests procedure
===

1. Run ./batch.py ns ns2 linux linux2 (which will run unit_test.sh -> test_ns3
   and merge pcaps from same node)
#. then ./per_pcap_plot.sh to generate per pcap
#. boxplot.py to generate boxplots
