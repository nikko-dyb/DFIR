Magnet Virtual Summit CTF iOS 2023 Write-up


1. A Few Too Many (5 points)

Question: How many email accounts did the user own? (Not counting privaterelay)
Answer: 5
Analysis: Navigated to user accounts under refined results and identified four different emails:

blueisth3best@gmail.com

borchardtmichael78@gmail.com

michaelkborchardt@proton.me

mborchardt@kurvalis.com

![Description](imagee/1.jpg)

Additionally, checked under "web-related" and "communications" to ensure nothing was missed.

2. Autofill Me on the Deets (5 points)

Question: Which email, other than their own, was autofilled in Chrome?
Answer: tlouis@kurvalis.com
Analysis: Located directly in the Chrome autofill artifact.

![Description](imagee/2.jpg)


3. 1 Fish 2 Fish, Red Fish Blue (5 points)

Question: According to the user’s email accounts, what is his favourite color?
Answer: Blue
Analysis: The email "blueisth3best@icloud.com" indicated a preference for blue.

![Description](imagee/3.jpg)


4. Q-usestion (5 points)

Question: What Chinese networking website was associated with LinkedIn?
Answer: Qzone
Analysis: Initially confused by the question, searched social media URLs under refined results. The LinkedIn keyword filter revealed a URL containing "Qzone," which was confirmed via a quick Google search.

![Description](imagee/qxone.jpg)

5. Chef Boyardee (10 points)

Question: At which market was the user viewing Chef Pasquale tomato sauce?
Answer: Marché Atwater
Analysis: Found in the photos artifact. Extracted EXIF data to determine latitude and longitude, confirming the location via Google Maps.

![Description](imagee/5.jpg)


6. Staying Stylish! (10 points)

Question: What color shirt did the user choose to put their Snapchat Bitmoji in?
Answer: Green
Analysis: Searched Snapchat contacts artifact and found the username "m_b227468." Using Snapchat, manually verified the Bitmoji color as green.

![Description](imagee/6.jpg)

![Description](imagee/61.jpg)


7. Picking Up Steam (10 points)

Question: What server was the user interested in making?
Answer: Rust/CS:GO server
Analysis: Noticed Rust and CS:GO while reviewing Google searches and open tabs.

![Description](imagee/7.jpg)


8. Overlooking Excellence (10 points)

Question: What sports stadium was the user overlooking at Camille-Houde Belvedere?
Answer: Stade Olympique
Analysis: Initially used Google Maps Street View but later confirmed the location through geotagged photos.

![Description](images/maps.jpg)

![Description](images/stadium.jpg)

![Description](images/statium.jpg)


9. You’re Going to Crush This One! (10 points)

Question: What light-hearted game did the user spend the most time on?
Answer: Candy Crush
Analysis: Identified through application usage artifacts.

![Description](images/9.jpg)


10. You Are Here (16 points)

Question: Which airline lounge was viewed?
Answer: Found via keyword search for "lounge" in Apple Maps.

![Description](images/10.jpg)


11. Out of This World (25 points)

Question: Which terms and conditions site on TikTok is named after a space formation?
Answer: Identified by cross-referencing TikTok terms and conditions with space-related keywords (e.g., Galaxy, Nebula, Black Hole, Supernova).

![Description](images/11.jpg)


12. Which Way? (25 points) 

Question: Which cardinal direction was the user turning when driving towards RHEINFAHRE?
Answer: South
Analysis: Extracted EXIF data from photos, confirmed location in Google Maps, and used the compass tool to determine direction.

![Description](images/rein.jpg)

![Description](images/reinfare.jpg)

13. Boosting into a New Era (25 points)

Question: The user was trying to learn German through an application, what promotion featuring a rocket was most commonly shown to the user?
Answer: Duolingo rocket promotion
Analysis: Searched "Duolingo" and "rocket" in media artifacts. Initially found "nudge rocket," but later discovered the correct promotion in a video artifact.

![Description](images/duoling.jpg)

![Description](images/duolingo.jpg)

14. As a River Runs (50 points)

Question: At which location did the user travel the most meters according to Apple? (City, Country)
Answer: Eltville, Germany
Analysis: Used Apple Health artifacts to identify maximum distance traveled, then correlated with cached location data from the relevant time period.

![Description](images/distance.jpg)

![Description](images/locationdistance.jpg)

15. Lo Siento Señor, It’s Going to Be a Cold One (50 points)

Question: What weather front was warned to the user by YouTube?
Answer: Frente Ártico
Analysis: Initially searched YouTube results with Spanish keywords. Found a news headline, "La llegada de un frente ártico hará que el 80% de EE.UU. experimente sensaciones térmicas congelantes." Though the original video was deleted, a related article on Univision confirmed the correct answer.

![Description](images/media.jpg)