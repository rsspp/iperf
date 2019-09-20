iPerf with support for SO_SHARDED SO_REUSEPORT and SO_AUTOMIGRATE


SO_REUSEPORT is the well known existing option to allow listening to the same socket from multiple processes. Note in this mode we also insert a BPF filter to send the packets received on core 0 to socket number 0. It makes sense only in the context of RSS++. Open one iPerf server per core in the right order (a cleaner implementation could be done using BPF maps, feel free to propose!).
SO_SHARDED use per-core socket tables, needs our modified kernel
SO_AUTOMIGRATE migrate the calling thread/process/task to where the last packet was received. It only makes sense if you manage correctly where packet are received (eg with RSS++)


Original README
---------------

This is Iperf v2.0.0, a tool for measuring Internet bandwidth performance.
See the doc directory for more documentation.
Briefly:

  ./configure      -- configure for your machine
  make             -- compile Iperf
  make install     -- install Iperf, if desired

  iperf -s               (on machine "foo.bar.edu")
  iperf -c foo.bar.edu   (on some other machine)
  iperf -h               (for help screen)
  iperf -v               (for version information)

Copyright 1999, 2000, 2001, 2002, 2003, 2004
The Board of Trustees of the University of Illinois
All rights reserved
See UI License (doc/ui_license.html) for complete details.

$Id: README,v 1.1.1.1 2004/05/18 01:50:44 kgibbs Exp $
