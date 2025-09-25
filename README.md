Rent Car Project
1. Introduction & Information
This is a Car Rental Management System built with modern web technologies. The project allows users to browse available cars, make rental orders, and manage their bookings. Admins can manage cars, users, and orders from the backend.

Key Features:

User authentication & authorization
Car listing with filtering (brand, fuel type, price, etc.)
Order management (create, cancel, complete)
Role-based access (admin, user)
2. Data Models
🏎️ Car
Field	Type	Description
id	UUID / int	Unique identifier
brand	string	Car brand (e.g., Toyota, BMW)
model	string	Car model (e.g., Corolla, X5)
price_per_day	decimal	Price per day for rental
engine_type	string	Petrol / Diesel / Hybrid / Electric
fuel_type	string	Gasoline, Diesel, Electric, etc.
shape_type	string	Sedan, SUV, Coupe, etc.
doors	int	Number of doors
seats	int	Number of seats
air_condition	boolean	Whether car has AC
distance	int	Mileage (km)
equipments	array[string]	Additional equipment (GPS, baby seat, etc.)
images	array[string]	Car images
available	boolean	Availability status
👤 User
Field	Type	Description
id	UUID / int	Unique identifier
name	string	Full name
email	string	Unique email
password	string	Hashed password
phone	string	Phone number
role	enum	admin or user
created_at	datetime	Account creation date
📄 Order
Field	Type	Description
id	UUID / int	Unique identifier
user_id	FK(User)	The customer
car_id	FK(Car)	The rented car
order_date	datetime	Start of rental
end_date	datetime	End of rental
total_price	decimal	Calculated = (days × car.price_per_day)
status	enum	pending, confirmed, cancelled, completed
payment_status	enum	paid, unpaid, refunded
created_at	datetime	Order creation date
3. API Design
Authentication
POST /api/auth/register → Register new user
POST /api/auth/vefify → Verification user
POST /api/auth/login → User login (JWT token)
GET /api/auth/me → Get logged-in user info
Cars
GET /api/cars → List all available cars (with filters: brand, price range, fuel type, seats, etc.)
GET /api/cars/:id → Get car details
POST /api/cars → Add a new car (admin only)
PUT /api/cars/:id → Update car info (admin only)
DELETE /api/cars/:id → Delete a car (admin only)
Orders
GET /api/orders → List orders (admin → all, user → own orders only)
GET /api/orders/:id → Get order details
POST /api/orders → Create a new order (requires: car_id, order_date, end_date)
PUT /api/orders/:id/cancel → Cancel order (user or admin)
PUT /api/orders/:id/confirm → Confirm order (admin only)
PUT /api/orders/:id/complete → Mark as completed (admin only)
Users (Admin Only)
GET /api/users → List all users
GET /api/users/:id → Get user details
DELETE /api/users/:id → Delete user
