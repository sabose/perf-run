# Comparison of performance accessing a virtual block device in oVirt via fuse vs libgfapi
 
Virtual machines were created in oVirt and used gluster volume as storage domain to store the virtual disks.
The iozone results posted are comparing the performance when the virtual block devicec stored in gluster volume are
accessed via fuse protocol vs gfapi using the qemu gluster gfapi driver. 
A vdsm build using [patch](https://gerrit.ovirt.org/44061) was used to test this.
Baseline = fuse

iozone was run on the guest accessing the mounted filesystem (/data) on virtual block device
    #!/bin/bash

    for i in {1..5}; do
	echo "========================================="
	echo "loop $i started"
	date
	/root/iozone3_465/src/current/iozone -a -f /data/testfile -n 4k -g 1024m > /root/iozone_results/test_fuse.${i}.iozone
	sleep 60
	echo "========================================="
    done

The iozone results comparison was generated using [iozone-results-comparator](https://github.com/pbenas/iozone-results-comparator)
