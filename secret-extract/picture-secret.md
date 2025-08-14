# Steghide

$sudo apt install steghide

$steghide --help

$steghide --embed -cf picture.jpg -ef file.txt

$steghide --info picture.jpg

$steghide --extract -sf picture.jpg

# Binwalk

$binwalk -h

$binwalk picture.jpg

$binwalk -e picture.jpg

$binwalk -W picture.jpg
