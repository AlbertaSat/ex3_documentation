# Scheduler Primer

### Basic Information
* A scheduler is defined as the process that assigns resources (usually processors -- it decides which process gets to run on the CPU) to perform tasks (adapted from [Wikipedia](https://en.wikipedia.org/wiki/Scheduling_(computing)))
   * Different schedulers have different design goals (maximizing throughput, minimizing wait time, minimizing response time, maximizing fairness, *etc.*) depending on the application
   * Process schedulers determine what process gets to run on the CPU and can be used to give some concurrency and multi-tasking on a single CPU
* Completely Fair Scheduler (CFS) is the process scheduler used by Linux
   * Uses red-black (rb) trees to prioritize processes that have spent the least time executing so far; new processes are seleced each time the current one blocks, terminates, or reaches its maximum execution time (waiting time divided by processor count)
   * Prioritizes fairness in that each process gets an even slice of CPU time and processes with the least runtime so far are given the CPU

***

# Summary of Previous Timing Research

### Problem Background
* We need to have a way to tell IRIS (the on-board camera) to take photos at particular intervals with great precision (roughly down to the millisecond), and these pictures must be scheduled repeatedly and generally predictably
* The satellite is moving at 7 km/s, so being off by even a small amount of time can cause the photo to be of a different location on Earth or blurry, and therefore useless
* This wasn’t really a problem for Ex-Alta 2 because the version of IRIS on that satellite had a resolution where one pixel was >7 km wide, but the new version of IRIS may have a significantly better resolution

### Possible Solutions
* Use the Linux scheduler to schedule this event
   * Basic info about the Linux scheduler is [here](https://en.wikipedia.org/wiki/Completely_Fair_Scheduler)
   * Robert recommends against this because it is risky to play with such dangerous low level details and would probably be overkill (plus it may be a lot of work), although some understanding and interaction with the scheduler will be necessary
* Use cron, a job scheduler for Unix-like systems that has been brought up as a possible solution
   * Basic info and background is [here](https://en.wikipedia.org/wiki/Cron)
   * Usually used for repetitive tasks, like fetching new emails every so often
   * Widely used and has existed since the 1970s, so proven and dependable at least for the intended use cases
   * Fairly simple syntax and use, just specify the minute, hour, day of month, year, and day of week for a particular command to be run in a cron table file (crontab), then the cron daemon runs those commands at the specified time
   * More information on cron in general is in the man page [here](https://man7.org/linux/man-pages/man8/cron.8.html) 
   * More information on crontabs in general is in the man page [here](https://man7.org/linux/man-pages/man5/crontab.5.html)
   * However, cron is not intended for high accuracy timing, only specifies down the minute -- actual timing when the commands are run is often off by a few seconds (as Robert said, making a new process is not ideal when trying to get precise timing)
   * Cron also does not provide much feedback about the execution of the process created (whether it was successful, how long it took, *etc.*) -- this makes it more difficult to communicate effectively with Fprime and other software
   * We could try to hack our own version that allows for millisecond precision (it seems some others have done this), but that is risky
   * There are some open-source third party alternatives that already exist like frequent-cron, the github repo for it is [here](https://github.com/homer6/frequent-cron), but this could be too risky
   * Some other built-in alternatives exist in Linux like systemd timers, wiki [here](https://wiki.archlinux.org/title/Systemd/Timers#As_a_cron_replacement) and man page [here](https://man.archlinux.org/man/systemd.timer.5), it seems like the accuracy of scheduling can be set as precise as 1 μs but it’s unclear whether it is this accurate in practice -- interesting comparisons of cron and systemd are [here](https://unix.stackexchange.com/questions/278564/cron-vs-systemd-timers)
* Making our own daemon process which can do this
   * Basic background and steps on making one are in man page [here](https://man7.org/linux/man-pages/man7/daemon.7.html)
   * Not sure how difficult or easy this would be, and also how reliable it would be
   * This obviously allows us to make its functionality support exactly what we need and nothing more which is valuable
* Using some version of the Ex-Alta 2 scheduler
   * Ground station documentation is [here](https://github.com/AlbertaSat/ex2_ground_station_software/blob/master/SCHEDULER.md), implementation of parser is [here](https://github.com/AlbertaSat/ex2_ground_station_software/blob/master/src/scheduleParser.py), they indicate that the scheduler has millisecond-level precision
   * The schedule does not use cron as far as I can tell, just the format of specifying times is similar to the format used for cron
   * Not sure how it relates to OBC scheduling code [here](https://github.com/AlbertaSat/ex2_obc_software/blob/master/ex2_services/Services/source/scheduler/scheduler.c) and [here](https://github.com/AlbertaSat/ex2_obc_software/blob/master/ex2_system/source/scheduler/scheduler_task.c), but it seems like it doesn’t really have millisecond level precision from code comments in there (*e.g.*, “Funny enough, the RTC doesn't have millisecond resolution, so the wait is ultimately specified in ticks!”, but I’m not sure if I’m misinterpreting that)
* Using Fprime built-in sequencer/scheduler
   * I don't think this is under consideration anymore, but if it is then I can pull out the data from experiments I've run and provide it
 
### Main Takeaways
* Cron may not be useful in our situation as it is not precise enough, but similar tools that overcome this problem exist -- they each come with their own weaknesses and risks, but systemd seems like a viable option
* Making a custom daemon to do this would obviously be the best solution for our case, but this comes with potentially significant risk and time investment
* More research should be done
