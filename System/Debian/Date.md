Dates / Times
------

#### Change Timezone
Unlink last timezone
`sudo unlink /etc/localtime`

Link new timezone
`sudo ln -s /usr/share/zoneinfo/${CURRENT_REGION}/${CURRENT_UTC_CITY}`

Check that time match with local time
`Watch your watch`
`time`
And compare
