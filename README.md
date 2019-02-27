# TCPBenchmarking
Checking on how different TCP variants perform in NS2 simulation. 

Completely based on paper “Simulation-based Comparisons of Tahoe, Reno, and SACK TCP” by Kevin Fall & Sally Floyd.

Simulate the network topology used by Fall and Floyd in their paper:

![alt](https://user-images.githubusercontent.com/12637959/53473831-7a6acf80-3a91-11e9-9b4c-3d02815a9bae.png)

Running simulations: (scripts, simulator code and output are attached)

Example: <TCP_TYPE> TCP - packet loss <no% of packet loss>:
1. Go in to tahoe folder and run ‘ns tcp_drop_tahoe.tcl <no% of packet loss>’
2. Based on <no% of packet loss> the output files will be created in the appropriate folder
3. Go in to the appropriate folder and run `cat out.tr | ../../Utils/packageplot.pl <TCP_TYPE>` . It must have created three output files (ack.tahoe, dropped.tahoe, sent.tahoe)
4. Go into gnuplot terminal by running `gnuplot`
5. Run the commands to plot the dropped packets, send packets and ack packets in graph and save as image
```
gnuplot
plot [0:6] "sent.tahoe" with points,"dropped.tahoe", "ack.tahoe" with dots 
set terminal pngcairo
set output 'output.png'
replot
unset output
```
6. For calculating avg.throughput and number of packets run  
`perl ../../Utils/throughputCalculator.pl out.tr 4 0.0 4.0 1.0`
![example](https://user-images.githubusercontent.com/12637959/53474269-a175d100-3a92-11e9-8ded-33a7857fb3fe.png)
7. For additional details, go to the site http://www.jgyan.com/analyzer/ and upload out.nam file
