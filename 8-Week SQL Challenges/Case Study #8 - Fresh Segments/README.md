```sql 

CREATE TABLE [User] (
    id INT PRIMARY KEY,
    full_name VARCHAR(255),
	role_id INT 
);

CREATE TABLE Category (
    id INT PRIMARY KEY,
    category_name VARCHAR(255)
);

CREATE TABLE Program (
    id INT PRIMARY KEY,
    user_id INT FOREIGN KEY REFERENCES [user](id),
    program_name VARCHAR(255),
    description VARCHAR(255),
    price FLOAT,
    category_id INT FOREIGN KEY REFERENCES category(id),
    asset_id INT
);

CREATE TABLE ProgramUser (
    program_id INT FOREIGN KEY REFERENCES program(id),
    user_id INT FOREIGN KEY REFERENCES [user](id),
    progress_percent FLOAT,
    status VARCHAR(50),
    startAt DATE,
    PRIMARY KEY (program_id, user_id)
);

CREATE TABLE ProgramSource (
    program_id INT FOREIGN KEY REFERENCES program(id),
    source_id INT,
    source_type_id INT,
    source_order INT,
    PRIMARY KEY (program_id, source_id, source_type_id)
);

CREATE TABLE ProgramMentor (
    program_id INT FOREIGN KEY REFERENCES program(id),
    user_id INT FOREIGN KEY REFERENCES [user](id),
    PRIMARY KEY (program_id, user_id)
);

CREATE TABLE Challenge (
    id INT PRIMARY KEY,
    category_id INT FOREIGN KEY REFERENCES category(id),
    challenge_name VARCHAR(255),
    description VARCHAR(255),
    location VARCHAR(255),
    phase VARCHAR(255),
    start_date DATETIME
);

CREATE TABLE ChallengeUser (
    challenge_id INT FOREIGN KEY REFERENCES challenge(id),
    user_id INT FOREIGN KEY REFERENCES [user](id),
    score FLOAT,
    status VARCHAR(255),
    date_submission DATETIME
);

CREATE TABLE Course (
    id INT PRIMARY KEY,
    course_name VARCHAR(255),
    description VARCHAR(255),
    price FLOAT,
    user_id INT FOREIGN KEY REFERENCES [user](id)
);

CREATE TABLE Review (
    id INT PRIMARY KEY,
    source_id INT,
    user_id INT FOREIGN KEY REFERENCES [user](id),
    source_type_id INT,
    rating_star INT,
    content VARCHAR(255)
);

CREATE TABLE EventLog (
    id INT PRIMARY KEY,
    user_id INT FOREIGN KEY REFERENCES [user](id),
    source_id INT,
    source_type_id INT,
    event_time DATETIME
);

CREATE TABLE PaymentMethod (
    id INT PRIMARY KEY,
    method VARCHAR(255)
);

CREATE TABLE Voucher (
    id INT PRIMARY KEY,
    code VARCHAR(255),
    source_id INT,
    source_type_id INT,
    discount FLOAT,
    quantity INT,
    expire_date DATETIME
);

CREATE TABLE UserPayment (
    id INT PRIMARY KEY,
    user_id INT FOREIGN KEY REFERENCES [user](id),
    card_name VARCHAR(255),
    card_number VARCHAR(255),
    expire_date DATETIME,
    PaymentMethod_id INT FOREIGN KEY REFERENCES PaymentMethod(id)
);

CREATE TABLE [Order] (
    id INT PRIMARY KEY,
    user_id INT FOREIGN KEY REFERENCES [user](id),
    user_payment_id INT FOREIGN KEY REFERENCES UserPayment(id),
    status VARCHAR(255),
    created_at DATETIME
);

CREATE TABLE OrderDetails (
    id INT PRIMARY KEY,
    order_id INT FOREIGN KEY REFERENCES [order](id),
    source_id INT,
    source_type_id INT
);

INSERT INTO [User] (id, full_name, role_id) VALUES
(1, 'Alice', 3),
(2, 'Bob', 3),
(3, 'Charlie', 3),
(4, 'David', 3),
(5, 'Eve', 2),
(6, 'Frank', 2),
(7, 'Grace', 3),
(8, 'Heidi', 3),
(9, 'Ivan', 3);

INSERT INTO Category (id, category_name) VALUES
(1, 'Information Technology'),
(2, 'UI/UX Design'),
(3, 'Marketing'),
(4, 'Lifestyle'),
(5, 'Photography'),
(6, 'Video');

INSERT INTO Program (id, user_id, program_name, description, price, category_id, asset_id) VALUES
(1, 5, 'Software Engineering Fundamentals', 'Essential software engineering concepts', 33.99, 1, 101),
(2, 6, 'Data Science', 'Data analysis and machine learning mastery', 12.99, 1, 102),
(3, 5, 'Web Development Mastery', 'Interactive e-learning platform', 17.77, 1, 103),
(4, 6, 'Mentoring Hub', 'Personalized professional growth through mentorship', 19.99, 3, 104),
(5, 5, 'Digital Marketing Bootcamp', 'Comprehensive training in digital marketing strategies and tools', 99.99, 2, 105),
(6, 1, 'Machine Learning A-Z', 'Complete machine learning guide', 45.99, 1, 106),
(7, 2, 'Cloud Computing Basics', 'Introduction to cloud services and architecture', 29.99, 4, 107),
(8, 2, 'Cybersecurity Essentials', 'Fundamentals of cybersecurity practices', 39.99, 3, 108),
(9, 3, 'Advanced Java Programming', 'Deep dive into Java programming language', 55.00, 1, 109),
(10, 4, 'Blockchain and Cryptocurrency', 'Understanding blockchain technology and cryptocurrencies', 60.00, 4, 110),
(11, 5, 'Artificial Intelligence for Beginners', 'Basics of AI and its applications', 70.00, 1, 111),
(12, 3, 'Project Management Professional (PMP)', 'Comprehensive PMP certification prep', 80.00, 5, 112),
(13, 4, 'User Experience (UX) Design', 'Designing user-friendly interfaces', 50.00, 2, 113),
(14, 5, 'Mobile App Development with Flutter', 'Building mobile apps using Flutter', 65.00, 4, 114),
(15, 1, 'DevOps and Continuous Integration', 'Introduction to DevOps practices and tools', 75.00, 1, 115);

INSERT INTO Course (id, course_name, description, price, user_id) VALUES
(1, 'Grow Your Video Editing Skills from Experts', 'Essential software engineering concepts', 7.99, 1),
(2, 'Easy and Creative Food Art Ideas Decoration', 'Data analysis and machine learning mastery', 5.99, 2),
(3, 'Create Your Own Sustainable Fashion Style', 'Interactive e-learning platform', 6.29, 3),
(4, 'Grow Your Skills Fashion Marketing', 'Personalized professional growth through mentorship', 5.99, 4),
(5, 'UI Design, a User-Centered Approach', 'Comprehensive training in digital marketing strategies and tools', 6.39, 5);

INSERT INTO Challenge (id, category_id, challenge_name, description, location, phase, start_date) VALUES
(1, 1, 'Image Classification', 'The challenge is to develop a deep learning model', 'Remote', 'Starting Phase', '2024-06-26'),
(2, 1, 'Fraud Detection Kaggle', 'Participate in a Kaggle competition', 'HCM', 'Starting Phase', '2024-06-27'),
(3, 5, 'Short Story Writing', 'Writing a compelling short story', 'Remote', 'Starting Phase', '2024-06-23'),
(4, 1, 'Data Prediction', 'Predicting data trends using ML', 'Remote', 'Ending Phase', '2024-06-27'),
(5, 5, 'Recipe Development', 'Creating new and innovative recipes', 'Remote', 'Ending Phase', '2024-06-23'),
(6, 1, 'E-commerce Website', 'Develop a full-stack e-commerce website', 'Remote', 'Starting Phase', '2024-07-01'),
(7, 1, 'Sentiment Analysis', 'Analyze sentiment from social media data', 'Remote', 'Starting Phase', '2024-07-01'),
(8, 2, 'Mobile App Design', 'Design a mobile app for a retail store', 'Remote', 'Starting Phase', '2024-07-01'),
(9, 3, 'Email Marketing Campaign', 'Create an effective email marketing campaign', 'Remote', 'Starting Phase', '2024-07-01'),
(10, 4, 'Personal Finance Blog', 'Write blog posts about personal finance', 'Remote', 'Starting Phase', '2024-07-01'),
(11, 5, 'Food Photography', 'Capture high-quality photos of food dishes', 'Remote', 'Starting Phase', '2024-07-01'),
(12, 6, 'Short Film Editing', 'Edit a short film with provided footage', 'Remote', 'Starting Phase', '2024-07-01'),
(13, 1, 'Real-time Chat Application', 'Build a real-time chat application', 'Remote', 'Starting Phase', '2024-07-01'),
(14, 2, 'Landing Page Optimization', 'Optimize the landing page of a website', 'Remote', 'Starting Phase', '2024-07-01'),
(15, 5, 'Travel Vlog', 'Create a travel vlog with provided footage', 'Remote', 'Starting Phase', '2024-07-01');

INSERT INTO Review (id, source_id, user_id, source_type_id, rating_star, content) VALUES
(1, 2, 1, 3, 3, 'Excellent tool for tracking environmental impact.'),
(2, 2, 2, 3, 4, 'Very helpful for managing patient records.'),
(3, 2, 3, 3, 4, 'Great platform for learning new skills.'),
(4, 4, 4, 3, 4, 'Useful for financial planning.'),
(5, 5, 5, 3, 5, 'Perfect place to showcase handmade products.'),
(6, 1, 1, 2, 4, 'Very insightful introduction to quantum computing.'),
(7, 2, 2, 2, 4, 'Comprehensive digital marketing strategies.'),
(8, 1, 3, 2, 3, 'Great exercises and peer reviews.'),
(9, 2, 4, 2, 3, 'Good coverage of data science techniques.'),
(10, 2, 5, 2, 5, 'Excellent culinary skills development.'),
(11, 1, 1, 1, 5, 'Challenging yet rewarding.'),
(12, 2, 2, 1, 4, 'Learned a lot about social media marketing.'),
(13, 2, 3, 1, 5, 'Fun and engaging short story writing tasks.'),
(14, 1, 4, 1, 5, 'Useful for improving data prediction skills.'),
(15, 1, 5, 1, 5, 'Inspired me to create new recipes.');

INSERT INTO ProgramSource (program_id, source_id, source_type_id, source_order) VALUES
(2, 1, 1, 1),
(2, 2, 1, 3),
(3, 3, 1, 3),
(4, 4, 1, 4),
(5, 5, 1, 5),
(2, 1, 2, 2),
(2, 2, 2, 4),
(3, 3, 2, 8),
(4, 4, 2, 9),
(5, 5, 2, 10);

INSERT INTO ProgramMentor (program_id, user_id) VALUES
(1, 1),
(1, 2),
(2, 3),
(2, 6),
(3, 4),
(3, 5);

INSERT INTO ProgramUser (program_id, user_id, progress_percent, status, startAt) VALUES
(1, 1, 50, 'In Progress', '2024-01-01'),
(2, 2, 30, 'In Progress', '2024-02-01'),
(3, 3, 80, 'Completed', '2024-03-01'),
(2, 1, 69, 'In Progress', '2024-04-01'),
(4, 2, 61, 'In Progress', '2024-05-01'),
(4, 3, 99, 'Completed', '2024-06-01'),
(5, 6, 81, 'Completed', '2024-07-01'),
(5, 7, 72, 'In Progress', '2024-08-01'),
(1, 2, 60, 'In Progress', '2024-07-10'),
(2, 3, 45, 'In Progress', '2024-06-15'),
(3, 4, 90, 'Completed', '2024-07-20'),
(1, 5, 70, 'In Progress', '2024-07-05'),
(5, 2, 95, 'Completed', '2024-06-23'),
(3, 1, 50, 'In Progress', '2024-07-12'),
(4, 1, 60, 'In Progress', '2024-07-08'),
(5, 1, 70, 'In Progress', '2024-07-15'),
(1, 3, 80, 'Completed', '2024-07-25'),
(2, 4, 90, 'Completed', '2024-07-30')


INSERT INTO ChallengeUser (challenge_id, user_id, score, status, date_submission) VALUES
(1, 1, 8, 'Passed', '2024-06-10'),
(2, 1, 6, 'Passed', '2024-05-08'),
(3, 2, 7, 'Passed', '2024-01-23'),
(4, 2, 3, 'Failed', '2024-02-04'),
(5, 3, 5, 'Passed', '2024-08-14'),
(3, 3, 4, 'Failed', '2024-12-17');

INSERT INTO EventLog (id, user_id, source_id, source_type_id, event_time) VALUES
(1, 1, 1, 3, '2024-03-02 00:00:00'),
(2, 1, 1, 1, '2024-03-03 00:00:00'),
(3, 1, 3, 2, '2024-04-04 00:00:00'),
(4, 1, 2, 3, '2024-05-05 00:00:00'),
(5, 3, 2, 1, '2024-06-06 00:00:00'),
(6, 1, 4, 3, '2024-07-07 00:00:00'),
(7, 1, 5, 3, '2024-08-08 00:00:00'),
(8, 1, 3, 3, '2024-09-09 00:00:00'),
(9, 1, 1, 3, '2024-03-05 00:00:00'),
(10, 1, 2, 1, '2024-03-06 00:00:00'),
(11, 1, 3, 2, '2024-04-07 00:00:00'),
(12, 1, 4, 3, '2024-05-08 00:00:00'),
(13, 2, 2, 1, '2024-06-09 00:00:00'),
(14, 2, 4, 3, '2024-07-10 00:00:00'),
(15, 2, 5, 3, '2024-08-11 00:00:00'),
(16, 2, 3, 3, '2024-09-12 00:00:00'),
(17, 3, 1, 3, '2024-03-11 00:00:00'),
(18, 3, 2, 1, '2024-03-12 00:00:00'),
(19, 3, 3, 2, '2024-04-13 00:00:00'),
(20, 3, 4, 3, '2024-05-14 00:00:00');

INSERT INTO PaymentMethod (id, method) VALUES
(1, 'Visa'),
(2, 'Credit / Debit Card');

INSERT INTO Voucher (id, code, source_id, source_type_id, discount, quantity, expire_date) VALUES
(1, 'DISCOUNT10', 1, 3, 10.0, 100, '2024-12-31 23:59:59'),
(2, 'SAVE20', 2, 3, 20.0, 50, '2024-11-30 23:59:59'),
(3, 'OFFER30', 3, 3, 30.0, 25, '2024-10-31 23:59:59'),
(4, 'PROMO15', 4, 3, 15.0, 200, '2024-09-30 23:59:59'),
(5, 'DEAL25', 5, 2, 25.0, 75, '2024-08-31 23:59:59');

INSERT INTO UserPayment (id, user_id, card_name, card_number, expire_date, PaymentMethod_id) VALUES
(1, 1, 'Mentee1223', '****1234', '2024-06-10', 1),
(2, 1, 'Mente4123', '****3232', '2024-06-10', 2);

INSERT INTO [order] (id, user_id, user_payment_id, status, created_at) VALUES
(1, 1, 1, 'Success', '2024-06-10 13:36:00'),
(2, 2, 2, 'Success', '2024-06-09 17:40:00'),
(3, 2, 2, 'Success', '2024-03-01 08:40:00'),
(4, 2, 2, 'Success', '2024-04-02 11:40:00'),
(5, 2, 2, 'Success', '2024-06-10 09:40:00');

INSERT INTO OrderDetails (id, order_id, source_id, source_type_id) VALUES
(1, 1, 1, 3),
(2, 1, 2, 3),
(3, 2, 2, 3),
(4, 2, 4, 3),
(5, 2, 5, 3),
(6, 3, 1, 3),
(7, 3, 2, 3),
(8, 4, 5, 3);

CREATE TABLE CartItem (
    id INT PRIMARY KEY,
    user_id INT FOREIGN KEY REFERENCES [user](id),
    source_id INT,
    source_type_id INT
)

INSERT INTO CartItem (id, user_id, source_id, source_type_id) VALUES
(1, 1, 1, 3),
(2, 1, 2, 3),
(3, 2, 2, 3),
(4, 2, 4, 3),
(5, 2, 5, 3),
(6, 3, 1, 3),
(7, 3, 2, 3),
(8, 4, 5, 3);

CREATE TABLE Setting (
    id INT PRIMARY KEY,
    setting_type VARCHAR(255),
    setting_name VARCHAR(255),
    setting_value INT
);

INSERT INTO Setting (id, setting_type, setting_name, setting_value) VALUES
(1, 'SourceType', 'course', 1),
(2, 'SourceType', 'challenge', 2),
(3, 'SourceType', 'program', 3),
(4, 'Role', 'Admin', 1),
(5, 'Role', 'Mentor', 2),
(6, 'Role', 'Mentee', 3)

CREATE TABLE Tag (
    id INT PRIMARY KEY,
    tag_name VARCHAR(255)
);

INSERT INTO Tag(id, tag_name) VALUES
(1, 'Python'),
(2, 'Data Science'),
(3, 'Selenium'),
(4, 'Web Development'),
(5, 'React'),
(6, 'React Router'),
(7, 'Redux'),
(8, 'NextJS'),
(9, 'React Native'),
(10, 'Jupyter Notebook'),
(11, 'Machine Learning'),
(12, 'Cloud Computing'),
(13, 'Cybersecurity'),
(14, 'Java'),
(15, 'Blockchain'),
(16, 'Cryptocurrency'),
(17, 'Artificial Intelligence'),
(18, 'Project Management'),
(19, 'UX Design'),
(20, 'Flutter'),
(21, 'DevOps');

CREATE TABLE SourceTag (
    source_id INT,
    source_type_id INT,
    tag_id INT,
    PRIMARY KEY (source_id, source_type_id, tag_id)
);

INSERT INTO SourceTag (source_id, source_type_id, tag_id) VALUES
(1, 3, 4),
(2, 3, 2),
(2, 3, 11),
(3, 3, 4),
(3, 3, 5),
(3, 3, 6),
(3, 3, 7),
(3, 3, 8),
(3, 3, 9),
(4, 3, 18),
(5, 3, 4),
(6, 3, 2),
(6, 3, 11),
(7, 3, 12),
(8, 3, 13),
(9, 3, 14),
(10, 3, 15),
(10, 3, 16),
(11, 3, 17),
(12, 3, 18),
(13, 3, 19),
(14, 3, 20),
(15, 3, 21),
(1, 2, 4),
(1, 2, 5),
(2, 2, 4),
(2, 2, 6),
(3, 2, 4),
(3, 2, 5),
(3, 2, 6),
(3, 2, 7),
(3, 2, 8),
(3, 2, 9),
(4, 2, 4),
(4, 2, 5),
(4, 2, 6),
(5, 2, 4),
(5, 2, 5),
(5, 2, 6),
(6, 2, 4),
(6, 2, 5),
(6, 2, 7), 
(7, 2, 11),
(8, 2, 19),
(8, 2, 20),
(9, 2, 3),
(10, 2, 4),
(11, 2, 5),
(12, 2, 6),
(13, 2, 4),
(13, 2, 5),
(14, 2, 19),
(15, 2, 6);

CREATE TABLE SourceImage (
    id INT PRIMARY KEY,
    asset_id INT,
    source_id INT,
    source_type_id INT
);

INSERT INTO SourceImage (id, asset_id, source_id, source_type_id) VALUES
(1, 1, 1, 3),
(2, 2, 2, 1),
(3, 3, 3, 2),
(4, 4, 4, 3),
(5, 5, 5, 3),
(6, 6, 1, 3),
(7, 7, 2, 2),
(8, 8, 3, 2),
(9, 9, 4, 1),
(10, 10, 1, 3);

CREATE TABLE AdsProgram (
    program_id INT FOREIGN KEY (program_id) REFERENCES program(id),
    startAt DATETIME,
    endAt DATETIME 
);

INSERT INTO AdsProgram (program_id, startAt, endAt) VALUES
(1, '2024-07-01 00:00:00', '2024-07-31 23:59:59'),
(3, '2024-08-01 00:00:00', '2024-08-15 23:59:59'),
(5, '2024-07-15 00:00:00', '2024-08-15 23:59:59');

CREATE TABLE UserOnline (
    user_id INT FOREIGN KEY REFERENCES [user](id),
    online_date DATETIME,
    online_time VARCHAR(255)
)

INSERT INTO UserOnline (user_id, online_date, online_time) VALUES
(1, '2024-01-15', '08:30:00'),
(2, '2024-01-20', '09:00:00'),
(3, '2024-02-10', '09:15:00'),
(4, '2024-02-18', '09:45:00'),
(5, '2024-04-05', '10:00:00'),
(1, '2024-04-22', '08:30:00'),
(2, '2024-04-14', '09:00:00'),
(3, '2024-04-25', '09:15:00'),
(4, '2024-05-08', '09:45:00'),
(5, '2024-05-19', '10:00:00'),
(1, '2024-06-03', '10:30:00'),
(2, '2024-06-15', '11:00:00'),
(1, '2024-07-02', '11:30:00'),
(2, '2024-07-20', '12:00:00'),
(1, '2024-08-05', '12:30:00'),
(2, '2024-08-16', '10:30:00'),
(3, '2024-09-01', '11:00:00'),
(3, '2024-09-18', '11:30:00'),
(3, '2024-10-10', '12:00:00'),
(2, '2024-10-25', '12:30:00'),
(1, '2024-11-03', '08:30:00'),
(2, '2024-11-14', '09:00:00'),
(3, '2024-12-01', '09:15:00'),
(4, '2024-12-22', '09:45:00'),
(5, '2024-12-31', '10:00:00');

-- INSERT TABLE config (
--     id INT PRIMARY KEY,
--     config_type VARCHAR(255),
--     config_name VARCHAR(255),
--     config_value VARCHAR(255)  
-- );

-- INSERT TABLE config (id, config_type, config_name, config_value) VALUES 
-- (1, "Trending Program", "Growth in enrollments", 0.4),
-- (2, "Trending Program", "View Activity", 0.3),
-- (3, "Trending Program", "Average Rating", 0.3)

-- Create function to get config value

```