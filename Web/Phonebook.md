# IP: 159.65.62.99:32192

### SITE

![phonebook-site-htb](https://user-images.githubusercontent.com/98345027/189274770-c7a4e005-e56b-4aee-aca0-d7b1ee078803.png)


##### Source Page
![Phonebook-htb-source-page](https://user-images.githubusercontent.com/98345027/189275920-5b1f9243-0c0c-41fa-a90d-c93af25c662c.png)

### Findings
```javascript
1.From Source Page we saw that we can login using  username and password as " Reese "
2.After trying multiple times with default  credentials, we cannot get logged into phonebook
3.Trying username and password as "Reese" doesn't work well.
4. So Trying  Wildcard ' * ' into username and password redirect to Search page

```
##### Burpsuite Login page

![burpsuite-phonebook-htb-login](https://user-images.githubusercontent.com/98345027/189276694-5083d36e-2543-44a7-98f4-6970d23d8445.png)


#### Search Page
![phone-book-redirect-search-htb](https://user-images.githubusercontent.com/98345027/189276860-de4d1a1e-df6a-4a02-86d2-ecb5e51438cc.png)

```javascript
1.After Redirected to Search Page of login, In the Search parameter searching each and every string  like (hello,admin and etc) doesn't output anything but as I put the username " Reese " .
2.The Webpage display the Credentials(Fullname,email and phone-number)
```
###### Credentials Display
![phone-book-searchpage-reese-htb](https://user-images.githubusercontent.com/98345027/189277431-2d073456-18cf-414d-97ae-26e01c0c9de0.png)

```javascript
Credentials
Kyle Reese	reese@skynet.com	555-1234567
```
```javascript
In Search query when I entered a space charcter it result me a long list of credentials which doesn't reveal the password of Reese
```
![phone-book-htb-adding space](https://user-images.githubusercontent.com/98345027/189278870-93f16711-a60f-4ded-9079-d1c8ae58f827.png)
