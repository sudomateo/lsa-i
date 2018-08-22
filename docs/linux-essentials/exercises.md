# Exercises

1. Change into the `/tmp` directory using the command `cd /tmp`.
2. Confirm you are in the `/tmp` directory using the command `pwd`.
3. Change back into your home directory using the command `cd`.
4. Confirm you are in your home directory using the command `pwd`.
5. Print the text `This is file01.` to the file `/tmp/file01` using the command `echo "This is file01." > /tmp/file01`.
6. Confirm the `/tmp/file01` file has the correct content using the command `cat /tmp/file01`.
7. Append the text `This is appended.` to the file `/tmp/file01` using the command `echo "This is appended." >> /tmp/file01`.
8. Confirm the `/tmp/file01` file has the updated content using the command `cat /tmp/file01`.
9. Send the output of the `printenv` command to a new file named `/tmp/myenv` using the command `printenv > /tmp/myenv`.
10. View the first five lines of the `/tmp/myenv` file using the command `head -n 5 /tmp/myenv`.
11. Declare and export a new environment variable with the command `export COURSE_NAME="LSA1"`.
12. Verify your newly exported environment variable exists using the command `printenv | grep COURSE_NAME`.
13. Practice these and other commands until you feel comfortable with them.
14. When finished, use the `exit` command to exit the shell and logout.
