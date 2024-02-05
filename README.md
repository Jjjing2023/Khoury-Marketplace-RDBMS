# Khoury-Marketplace-RDBMS

## Abstraction

The Khoury Marketplace System is a database system and application devolved using MySQL running on Google Cloud Platform (GCP), and the user interface is developed using Python and Django. At its core, this marketplace serves as a versatile platform where users can register and participate in buying and selling activities. It offers an array of features, including secure messaging for seamless communication, detailed item listings with bidding options, flexible payment and shipping methods, user ratings to enhance trustworthiness, and efficient shopping cart and checkout functionality.
Database users can utilize the capabilities by generating daily/weekly reports, managing user profiles, overseeing messages, and accessing comprehensive auction and transaction data. Advanced queries provide insights into trending items, user activity, dispute resolution, payment/shipping status, and marketplace performance metrics. These features collectively enhance query experiences and streamline marketplace management.

## step 1

Project Name: Khoury Marketplace System
Group members: Fan Zhou, Jiawei Liu, Tianjing Liu, Yu-En Wang
We plan to build a web-based system in with Python and Django. Database system based on RDBMS, specifically MySQL on GCP. The users can sell and bid the items in the Khoury Marketplace.

## Minimum Requirements

1. There are two types of users: "Admin" and "Normal" users.
   - Admin user: can manage the entire system, so can access any addition. Admin users can access daily/weekly reports.
   - Normal user can be both "Seller" and "Bidder."
2. Normal users can register in the system and then sign in.
3. Normal users can be sellers, so they can post a new auction item.
4. Another normal user can bid on any item.
5. Payment system can be offline, such as a personal check.
6. Shipping system can create UPS tracking numbers.
7. Winners and sellers can rate the service each other.
8. Any users can see each user profile.
9. Normal user can send a message to other users regarding the bidding item.
10. Normal user can send a message to the Admin user regarding any issue on the item.
11. Admin user can see and receive the message and related items.

## Additional Requirements:

12. Users can reset account passwords.
13. Users can put multiple merchandise into their shopping cart.
14. Sellers can post pictures and text.
15. Sellers can enable location.
16. Sellers can see all the bidders, offered prices, and their profiles (including their rating).
17. Sellers can specify starting price, bid start time, and end time.
18. Sellers can specify the delivery method, such as UPS delivery, pick up, or meetup.
19. Sellers can specify the payment method, such as cash or personal check.
20. Buyers can set filters on things they are looking for.
21. Buyers can see the bidding history, and buyers can adjust the price before the final deadline.
22. Sellers can edit the products (e.g., delete or edit the name of the product and description).
23. Sales Management for sellers (e.g., sellers can see sales details and records and make shipping).
24. Allow buyers to save a selling item and enable notification when bidding starts.
25. Checkout information validation (review) before buyers placing an order.
26. Auto-fill checkout information from buyers’ 2nd order.
27. Order Management for buyers (e.g., View orders and order status).
28. Implement filters for price range, product categories, seller ratings, etc.

## UML Diagram:

![UML Diagram](https://github.com/Jjjing2023/Khoury-Marketplace-RDBMS/blob/main/images/uml_diagram.jpg?raw=true)

## Step 3

### For Normal Users (Sellers and Bidders)

1.Showing a List of Auction Items: Retrieve a list of all active auction items along with their details (item name, description, starting bid, current highest bid, time left for the auction).
2.Finding Bid History of a Specific Item: Display the bid history for a specific item, showing bidder usernames and bid amounts. 3. Fetch a specific user Auctions: Fetch a list of all auction items posted by a specific user (as a seller).
4.Bid status: Check the status of a user's bid on a specific item (winning, outbid, or auction ended). 5. View user’s profile: View the profile of a specific user, including their rating, active auctions, and won auctions.
6.Send Message to Seller: Send a message to the seller regarding a specific auction item.
7.Send Message to Admin: Send a message to the admin regarding an issue with an item or transaction.
8.Rate Transaction: Submit a rating for a transaction after an auction concludes, as a seller or a winner.
9.Search Items: Search for auction items based on keywords, categories, or specific seller usernames.

### For Admin Users

10.Daily/Weekly Reports: Generate reports summarizing the number of auctions, bids made, successful transactions, and user activity for the day/week.
11.User Management: View, edit, or delete user profiles, including resetting passwords or suspending accounts for misconduct.
12.Message Overview: Access and manage messages sent by users to the admin, including issues, complaints, or suggestions.
13.System-wide Auction Overview: Retrieve a list of all active auctions, including item details, current highest bids, and seller information.
14.Transaction History: Access detailed transaction history, including successful bids, payment methods used, and any disputes or ratings.

### Complex Queries for Advanced Insights

15.Trending Items: Identify items that receive the most bids or queries within a specific time frame.
16.User Activity Analysis: Analyze user activity to identify the most active buyers and sellers, peak bidding times, or popular item categories.
17.Dispute Resolution: Retrieve a list of transactions with disputes or low ratings for further investigation and resolution.
18.Payment and Shipping Status: Monitor the status of payments (received/pending) and shipping (dispatched/delivered), especially for transactions with personal checks or issues with tracking numbers.
19.Marketplace Performance Metrics: Calculate key performance indicators such as the average time to sell an item, average final bid amount versus starting bid, and seller ratings.

## Step 4

Assumptions about the database for the Marketplace system:

1. User Attributes:
   Users, including both Admin and Normal users, have attributes such as user_id (primary key), username, password, email, role (Admin, Seller, Bidder), and rating.
2. Item Attributes:
   Auction items posted by Sellers have attributes like item_id (primary key), item_name, description, starting_bid, current_highest_bid, bid_start_time, bid_end_time, and item_status.
3. Relationships:

- There is a many-to-many relationship between users and auction items, as a user can be both a Seller and a Bidder. This is represented through association tables for Seller_Items and Bidder_Items.
- There is a one-to-many relationship between Sellers and the auction items they post.
- Each bid on an item is associated with a Bidder and an Auction Item. 4. Keys:
- Primary keys are designated for each table (e.g., user_id for Users, item_id for Items).
- Foreign keys are used to establish relationships between tables (e.g., user_id in Seller_Items and Bidder_Items).

5. Message System:
   The Message entity has attributes like message_id (primary key), sender_id (foreign key referencing Users), receiver_id (foreign key referencing Users), message_content, and timestamp.
6. Rating System:
   Ratings are associated with transactions and have attributes like rating_id (primary key), rated_user_id (foreign key referencing Users), rating_value, and comments.
7. Shopping Cart:
   The Shopping Cart entity has attributes like cart_id (primary key), user_id (foreign key referencing Users), and item_id (foreign key referencing Items).
8. Checkout Information:
   Checkout information includes attributes such as checkout_id (primary key), user_id (foreign key referencing Users), item_id (foreign key referencing Items), and payment/shipping details.
9. Location Attribute:
   For Sellers, there is a location attribute to enable/disable location information associated with an item.
10. Notification System:
    Notification preferences for buyers regarding saved items and bidding activities are stored.
11. Filters and Preferences:
    Buyer filters, preferences, and saved searches are associated with user profiles.
12. Assumption on Password Reset:
    Users can reset their account password through a secure mechanism, potentially involving email verification.
13. Assumption on Auction Management:
    Sellers can edit their posted products, including deletion or modification of product name and description.
14. Assumption on Reports:
    Daily/weekly reports generated for Admin include summarized information on auctions, bids, transactions, and user activity.
15. Assumption on Payment and Shipping:
    The offline payment system (e.g., personal check) and shipping methods (e.g., UPS tracking) are managed for each transaction.
16. Assumption on User Activity Analysis:
    User activity analysis considers factors like peak bidding times and popular item categories.
