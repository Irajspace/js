# These are the packages we get in next js already
![alt text](nextjs-images/image.png)

# How does Root layout work check out
![alt text](nextjs-images/image-1.png)
Here you can see we are exporting a component called root layout
- the children automatically catches the 
![alt text](nextjs-images/image-2.png)
![alt text](nextjs-images/image-3.png)

# when we want to move to /about page through headers we can use a href 
![alt text](nextjs-images/image-4.png)
But this has his downside ... here pages gets to refresh
- Instead we can use Link tag
![alt text](nextjs-images/image-5.png)

# GOOD PRACTICE
- when you render any external component
- Make a component folder and make that component inside that
- Then import it
![alt text](nextjs-images/image-6.png)

# ROUTE URL 
 you can use (users) means u can use brackets around
 means you can simply localhost:3000/about -> will link to about page of users directly
 you dont need to add specifically :3000/users/about
 ![alt text](nextjs-images/image
-7.png)
 or you can use this
 ![alt text](nextjs-images/image
-8.png)

# nextjs-images/image component
![alt text](nextjs-images/image-9.png)
it can be easiky accesed thru /rishi.jpg if  it is public folder
- also can do lazy loading false if you keep priority-> false

# Font 
![alt text](nextjs-images/image-10.png)
multiple fonts
![alt text](nextjs-images/image-11.png)

# Metadata
![alt text](nextjs-images/image-12.png)
isse ye dikhega upar
![alt text](nextjs-images/image-13.png)
key words bhi matter krta hai
![alt text](nextjs-images/image-14.png)


# React CLient vs Server side components
    1) all event listeners must be on client side
    2) most database url when we are fetching must be taken from server side component
    3)all the components inside client page is automatically under client
![alt text](nextjs-images/image-15.png)
    4)

# Dynamic routes
![alt text](nextjs-images/image-16.png)
user/?? koi sa bhi name le skte hian/posts/ ??koi sab hi id
![alt text](nextjs-images/image-17.png)
THis is server side dynamic route
![alt text](nextjs-images/image-18.png)
if you want client side dynamic route then??
- we can use useapi
![alt text](nextjs-images/image-19.png)

# searchParams
for server side
![alt text](nextjs-images/image-20.png)
![alt text](nextjs-images/image-21.png)
![alt text](nextjs-images/image-22.png)

for client side
use useSearchParams

# Catch all segments

![alt text](nextjs-images/image-23.png)

# loading before real page
use simple loading.jsx

# fallback
![alt text](nextjs-images/image-24.png)
![alt text](nextjs-images/image-25.png)
![alt text](nextjs-images/image-26.png)