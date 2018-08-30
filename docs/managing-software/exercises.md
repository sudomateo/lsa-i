# Exercises

1. Install the `screen` package using the command `sudo yum install screen`. Press ++y++ if prompted.
2. Verify the screen package is installed using the command `sudo yum list installed | grep -i screen`. You should see the matching output.
3. Remove the `screen` package using the command `sudo yum remove screen`.
4. Verify the screen package is removed using the command `sudo yum list installed | grep -i screen`. You should see no matching output.
5. Run the command `ps aux` to view all of the processes currently executing on the system.
6. Run the command `top` to view all of the processes and their resource usage. Notice how the output refreshed every 2 seconds. Press ++q++ to quit when done looking around.
7. Run the command `sleep 60`. Press ++ctrl+c++ to quit the command early.
8. Run the command `sleep 15 &` to run `sleep` in the background. Run the `jobs` command to verify the background command is still running. Wait for 15 seconds and run the `jobs` command again to verify that the job is no longer executing in the background.
9. Run the command `sleep 600 &` to run the `sleep 600` command in the background. You will be shown the PID of the background process. Keep a note of this for the next steps.
    1.  Verify the PID exists using the command `ps aux | grep PID` where `PID` is the PID from earlier.
    2.  Use the `kill -15 PID` command where `PID` is the PID from earlier to send a `SIGTERM` command to that process.
    3.  Run the `jobs` command to verify your background process was terminated.
10. Run the command `sleep 444 &` to run the `sleep 444` command in the background. You will be shown the PID of the background process. Keep a note of this for the next steps.
    1.  Verify the PID exists using the command `ps aux | grep PID` where `PID` is the PID from earlier.
    2.  Use the `kill -9 PID` command where `PID` is the PID from earlier to send a `SIGKILL` command to that process.
    3.  Run the `jobs` command to verify your background process was killed.
11. Run the command `sudo yum install epel-release` to install the EPEL repository.
12. Run the command `sudo yum install nginx` to install the nginx webserver. Press ++y++ if prompted. 
13. Run the command `sudo systemctl status nginx` to see the status of the nginx webserver. It should show inactive or dead.
14. Run the command `sudo systemctl start nginx` to start the nginx webserver.
15. On your local workstation, open a web browser and navigate to `http://127.0.0.1:8080`. You should see an nginx test page.
16. Run the command `sudo systemctl stop nginx` to stop the nginx webserver.
17. Try to reload the web page on your local workstation. It should not load this time.
18. Verify the nginx service is not running using the command `sudo systemctl status nginx`.
19. Practice these and other commands until you feel comfortable with them.
20.  When finished, use the `exit` command to exit the shell and logout.
