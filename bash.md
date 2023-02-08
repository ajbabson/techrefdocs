
# Bash tips

<pre>
# check your shell options
shopt

type <command>, -all, -path, -type
hash
echo $SECONDS

# change to previous directory
cd -

# signifies the end of command options; positional arguments follow
--

# redirect stdout and stderr to file
command &> file

# redirect stderr to the same place as stdout, and send to command2
command 2>&1 | command2

# do the same thing as above
command |& command2

# append stderr along with stdout
command &>> file

# open file for reading with descriptor 7
exec 7< file.txt
# or writing
exec 7> file.txt

# open file for rw with descriptor 7
exec <>7 file.txt

# close file descriptor 7 for reading
exec 7<&-
# or writing
exec 7>&-

# exit status of the shell
$?

# PID of the shell
$$

# string comparison
[ $x == $y ]

# numeric comparison
[ $x -eq $y ]
# or 
((x==y))

# reading from a here doc
do
    read a b c d e <<END
    $(date)
END
echo $d

# indirection with !
x=abc
abc=def
echo ${!x} prints 'def'

# return default value if var is unset (but don't assign default value)
x=${var:-defaultvalue}

# same except also assign default value to var
x=${var:=defaultvalue}

# display error and exit if var is unset
x=${var:?}

# return nothing if var is unset (otherwise return var)
x=${var:+}

# return value start at position n
x=${var:n}

# take a slice from n, nn characters long
x=${var:n:nn}

# return length of var
x=${#var}

# remove from beginning of var
${var#pattern}

# remove from end of var
${var%pattern}

# check syntax
bash -u <script>

# run with debug
bash -x <script>

# toggle debugging inside script
set -x [+x]

# report use of unset variables (add to top of script)
set -u

# bash foo
tar zcvf - /home | ssh pinky "cat > inky-homes.tgz"
tar zcf - apache/ | ssh packman "cd /usr/local; mv apache apache.bak; tar zpxvf -"
ssh pinky "cd /usr/local/packland; tar zpvxf -" < really-big-archive.tgz
</pre>
