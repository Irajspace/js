# These are the packages we get in next js already
![alt text](image.png)

# How does Root layout work check out
![alt text](image-1.png)
Here you can see we are exporting a component called root layout
- the children automatically catches the 
![alt text](image-2.png)
![alt text](image-3.png)

# when we want to move to /about page through headers we can use a href 
![alt text](image-4.png)
But this has his downside ... here pages gets to refresh
- Instead we can use Link tag
![alt text](image-5.png)

# GOOD PRACTICE
- when you render any external component
- Make a component folder and make that component inside that
- Then import it
![alt text](image-6.png)

# ROUTE URL 
 you can use (users) means u can use brackets around
 means you can simply localhost:3000/about -> will link to about page of users directly
 you dont need to add specifically :3000/users/about
 ![alt text](image-7.png)
 or you can use this
 ![alt text](image-8.png)

# Image component
![alt text](image-9.png)
it can be easiky accesed thru /rishi.jpg if  it is public folder
- also can do lazy loading false if you keep priority-> false

# Font 
![alt text](image-10.png)
multiple fonts
![alt text](image-11.png)

# Metadata
![alt text](image-12.png)
isse ye dikhega upar
![alt text](image-13.png)
key words bhi matter krta hai
![alt text](image-14.png)


# React CLient vs Server side components
    1) all event listeners must be on client side
    2) most database url when we are fetching must be taken from server side component
    3)all the components inside client page is automatically under client
![alt text](image-15.png)
    4)

# Dynamic routes
![alt text](image-16.png)
user/?? koi sa bhi name le skte hian/posts/ ??koi sab hi id
![alt text](image-17.png)
THis is server side dynamic route
![alt text](image-18.png)
if you want client side dynamic route then??
- we can use useapi
![alt text](image-19.png)

# searchParams
for server side
![alt text](image-20.png)
![alt text](image-21.png)
![alt text](image-22.png)

for client side
use useSearchParams

# Catch all segments

![alt text](image-23.png)

# loading before real page
use simple loading.jsx

# fallback
![alt text](image-24.png)
![alt text](image-25.png)
![alt text](image-26.png)