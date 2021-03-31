sudo -l

find / -user root -perm 4000 -print 2>/dev/null
find / -type f -perm 04000 -ls 2>/dev/null

