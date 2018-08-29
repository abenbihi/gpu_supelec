## Login

    
## How to connect to a gpu from inside supelec
Connect to supelec server

    # ghome.metz.supelec.fr (193.48.224.129)
    mymachine:~:mylogin$ ssh benbihi_ass@ghome.metz.supelec.fr

In your working space called ~/ws/name (it can be the supelec server), clone the repository and make the scripts executables:

    ws:~:mylogin$ git clone git@192.93.8.150:sp/gpu_supelec.git
    ws:~:mylogin$ chmod u+x book.sh kill_reservation.sh log.sh port_forward.sh
    
The scripts allow you to:

    book.sh # book a GPU    
    kill_reservation.sh # free the reservation
    log.sh # log to the booked GPU
    port_forward.sh # activate port forwarding for Tensorboard
    
IMPORTANT:  
These scripts must be in the same directory. The book.sh script handles ONLY ONE
reservation, i.e. running it two times will simply kill the first reservation.

To book and log on a gpu, run the command below

    ws:~:mylogin$ ./book.sh mylogin i # i=0 if you are on the supelec server, 1 elseway 
    Booking a node
    Reservation successfull
    Booking requested : OAR_JOB_ID =  99785
    Waiting for the reservation to be running, might last few seconds
       The reservation is not yet running
       The reservation is not yet running
       The reservation is not yet running
       The reservation is not yet running
       [...]
       The reservation is not yet running
       The reservation is not yet running
       The reservation is running
    The reservation is running
    ws:~:mylogin$.

If the reservation is successfull, you can then log to the booked GPU:

    ws:~:mylogin$ ./log.sh mylogin i # i=0 if you are on the supelec server, 1 elseway
    The file job_id exists. I am checking the reservation is still valid
       The reservation is still running
    Logging to the booked node
    Connect to OAR job 99785 via the node sh11
    sh11:~:mylogin$
    
You end up with a terminal logged on a the GPU machine where you can execute your.
code. Your reservation will run for 24 hours. If you need more time, you may need 
o tweak the bash script a little bit.

You can log any terminal you wish to the booked machine.

Once your work is finished, just unlog from the machine and run kill_reservation.sh:

    sh11:~:mylogin$ logout
    Connection to sh11 closed.
    Disconnected from OAR job 99785
    Connection to term2.grid closed.
      Unlogged
    ws:/home/mylogin:mylogin$ ./kill_reservation.sh mylogin i # i=0 if you are on the supelec server, 1 elseway
     The file job_id exists. I will kill the previous reservation in case it is running
    Deleting the job = 99785 ...REGISTERED.
    The job(s) [ 99785 ] will be deleted in a near future.
    Waiting for the previous job to be killed
    Done
    ws:~:mylogin$
