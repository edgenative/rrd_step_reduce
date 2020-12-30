# rrd_step_reduce
Change the interval of an RRD file after its created.  This was originally found on a blog over at elturista.net, but that domain seems to be with someone else now, so the blog is gone.  Version here for safe keeping.

# Usage 

Dump your raw data into an XML file, using rrdtool dump
```bash
rrdtool dump file.rrd > file.15min.xml
```
Next, generate raw data with the new time interval. Specify the time reduction factor on the command line, in this example, I want a 5 min sample rate after originally having 15 mins.  So using a factor of 3 gives the right output.

```bash
./rrd_step_reduce.py file.15min.xml 3 > file.5min.xml
```

Backup your old file and remove it.  Then run rrdtool restore, to re-create an rrd file from your new xml data.

```bash
rrdtool restore file.5min.xml file.rrd
```

Modify the system you were using to generate the rrd data.

Profit.
