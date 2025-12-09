~~~~bash
echo "md5"$(echo -n "YOUR_STRONG_PASSWORD" | md5sum | awk '{print $1}')
~~~~