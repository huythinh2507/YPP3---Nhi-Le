```sql
CREATE TABLE MentorHub
GO

USE MentorHub
GO 

-- DROP FOREIGN KEYS
declare @sql nvarchar(max) = (
    select
    'alter table ' + quotename(schema_name(schema_id)) + '.' +
        quotename(object_name(parent_object_id)) +
        ' drop constraint '+quotename(name) + ';'
from sys.foreign_keys
for xml path('')
);
exec sp_executesql @sql;

DROP TABLE IF EXISTS Jobtitle
CREATE TABLE Jobtitle (
  id INT NOT NULL PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255)
);

DROP TABLE IF EXISTS Location
CREATE TABLE Location (
  id INT NOT NULL PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255)
);

DROP TABLE IF EXISTS [User]
CREATE TABLE [User] (
  id INT PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255),
  asset_id INT,
  location_id INT,
  jobtitle_id INT,
  role_id INT,
  create_at DATETIME,
  age INT,
  gender VARCHAR(10),
  status BIT,
  email varchar(255),
  dob date DEFAULT null,
  FOREIGN KEY (jobtitle_id) REFERENCES Jobtitle(id),
  FOREIGN KEY (location_id) REFERENCES Location(id)
);

DROP TABLE IF EXISTS SourceImage
CREATE TABLE SourceImage (
  id INT PRIMARY KEY IDENTITY(1,1),
  source_id INT,
  asset_id INT,
  source_type_id INT
);

DROP TABLE IF EXISTS Category
CREATE TABLE Category (
  id INT PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255)
);

DROP TABLE IF EXISTS Course
CREATE TABLE Course (
  id INT PRIMARY KEY IDENTITY(1,1),
  name NVARCHAR(255),
  category_id INT,
  price DECIMAL(10, 2),
  description TEXT,
  created_at DATETIME,
  mentor_id INT,
  pass_condition INT,
  thumbnail_id INT,
  FOREIGN KEY (category_id) REFERENCES Category(id),
  FOREIGN KEY (mentor_id) REFERENCES [User](id),
  FOREIGN KEY (thumbnail_id) REFERENCES SourceImage(id)
);

DROP TABLE IF EXISTS Ads
CREATE TABLE Ads (
  source_id INT PRIMARY KEY IDENTITY(1,1),
  source_type INT,
  thumbnail_id INT,
  start_at DATETIME,
  end_at DATETIME,
  FOREIGN KEY (thumbnail_id) REFERENCES SourceImage(id)
);

DROP TABLE IF EXISTS Tag
CREATE TABLE Tag (
  id INT PRIMARY KEY IDENTITY(1,1),
  tag_name VARCHAR(255)
);

DROP TABLE IF EXISTS SourceTag
CREATE TABLE SourceTag (
  source_id INT,
  source_type_id INT,
  tag_id INT
);

DROP TABLE IF EXISTS Section
CREATE TABLE Section (
  id INT PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255),
  course_id INT,
  FOREIGN KEY (course_id) REFERENCES Course(id)
);

DROP TABLE IF EXISTS Lesson
CREATE TABLE Lesson (
  id INT PRIMARY KEY IDENTITY(1,1),
  section_id INT,
  title VARCHAR(255),
  transcript TEXT,
  summary TEXT,
  asset_id INT,
  FOREIGN KEY (section_id) REFERENCES Section(id)
);

DROP TABLE IF EXISTS Resource
CREATE TABLE Resource (
  id INT PRIMARY KEY IDENTITY(1,1),
  asset_id INT,
  lesson_id INT,
  FOREIGN KEY (lesson_id) REFERENCES Lesson(id)
);

DROP TABLE IF EXISTS Discussion
CREATE TABLE Discussion (
  id INT PRIMARY KEY IDENTITY(1,1),
  user_id INT,
  lesson_id INT,
  parent_discussion_id INT,
  content TEXT,
  created_at DATETIME,
  FOREIGN KEY (user_id) REFERENCES [User](id),
  FOREIGN KEY (lesson_id) REFERENCES Lesson(id),
  FOREIGN KEY (parent_discussion_id) REFERENCES Discussion(id)
);

DROP TABLE IF EXISTS Review
CREATE TABLE Review (
    id INT PRIMARY KEY IDENTITY(1,1),
    source_id INT,
    user_id INT,
    source_type_id INT,
    rating_star INT,
    content VARCHAR(255),
	review_at TIME,
    FOREIGN KEY (user_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS MenteeSaveCourse
CREATE TABLE MenteeSaveCourse (
  course_id INT,
  mentee_id INT,
  FOREIGN KEY (course_id) REFERENCES Course(id),
  FOREIGN KEY (mentee_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS Progress
CREATE TABLE Progress (
  id INT PRIMARY KEY IDENTITY(1,1),
  lesson_id INT,
  mentee_id INT,
  course_id INT,
  time_closed DATETIME,
  status BIT,
  FOREIGN KEY (lesson_id) REFERENCES Lesson(id),
  FOREIGN KEY (mentee_id) REFERENCES [User](id),
  FOREIGN KEY (course_id) REFERENCES Course(id)
);

DROP TABLE IF EXISTS Voucher
CREATE TABLE Voucher (
  id INT PRIMARY KEY IDENTITY(1,1),
  code VARCHAR(255),
  source_id INT,
  source_type_id INT,
  discount FLOAT,
  quantity INT,
  expire_date DATETIME
);

DROP TABLE IF EXISTS PaymentMethod
CREATE TABLE PaymentMethod (
  id INT PRIMARY KEY IDENTITY(1,1),
  method VARCHAR(255)
);

DROP TABLE IF EXISTS UserPaymentInfo
CREATE TABLE UserPaymentInfo (
  id INT PRIMARY KEY IDENTITY(1,1),
  user_id INT,
  name_on_card VARCHAR(255),
  card_number VARCHAR(20),
  expiry_date DATETIME,
  payment_method_id INT,
  FOREIGN KEY (user_id) REFERENCES [User](id),
  FOREIGN KEY (payment_method_id) REFERENCES PaymentMethod(id)
);

DROP TABLE IF EXISTS [Order]
CREATE TABLE [Order] (
  id INT PRIMARY KEY IDENTITY(1,1),
  user_id INT,
  user_payment_id INT,
  status INT,
  created_at DATETIME,
  FOREIGN KEY (user_id) REFERENCES [User](id),
  FOREIGN KEY (user_payment_id) REFERENCES UserPaymentInfo(id)
);

DROP TABLE IF EXISTS OrderDetail
CREATE TABLE OrderDetail (
  id INT PRIMARY KEY IDENTITY(1,1),
  order_id INT,
  price DECIMAL(10, 2),
  source_id INT,
  source_type_id INT,
  FOREIGN KEY (order_id) REFERENCES [Order](id)
);

DROP TABLE IF EXISTS CartItem
CREATE TABLE CartItem (
  id INT PRIMARY KEY IDENTITY(1,1),
  user_id INT,
  source_id INT,
  source_type_id INT,
  FOREIGN KEY (user_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS Quiz
CREATE TABLE Quiz (
  id INT PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255),
  summary TEXT,
  attempts_allowed INT,
  passing_grade INT,
  duration TIME,
  section_id INT,
  FOREIGN KEY (section_id) REFERENCES Section(id)
);

DROP TABLE IF EXISTS QuestionType
CREATE TABLE QuestionType (
  id INT PRIMARY KEY IDENTITY(1,1),
  type VARCHAR(255)
);

DROP TABLE IF EXISTS Question
CREATE TABLE Question (
  id INT PRIMARY KEY IDENTITY(1,1),
  question_type_id INT,
  quiz_id INT,
  title TEXT,
  randomize BIT,
  points FLOAT,
  explanation TEXT,
  FOREIGN KEY (question_type_id) REFERENCES QuestionType(id),
  FOREIGN KEY (quiz_id) REFERENCES Quiz(id)
);

DROP TABLE IF EXISTS Answer
CREATE TABLE Answer (
  id INT PRIMARY KEY IDENTITY(1,1),
  question_id INT,
  content TEXT,
  asset_id INT,
  is_correct BIT,
  FOREIGN KEY (question_id) REFERENCES Question(id)
);

DROP TABLE IF EXISTS QuizResult
CREATE TABLE QuizResult (
  mentee_id INT,
  quiz_id INT,
  date DATETIME,
  mark FLOAT,
  result BIT,
  FOREIGN KEY (mentee_id) REFERENCES [User](id),
  FOREIGN KEY (quiz_id) REFERENCES Quiz(id)
);

DROP TABLE IF EXISTS MenteeQuestion
CREATE TABLE MenteeQuestion (
  mentee_id INT,
  question_id INT,
  earned_marks FLOAT,
  FOREIGN KEY (mentee_id) REFERENCES [User](id),
  FOREIGN KEY (question_id) REFERENCES Question(id)
);

DROP TABLE IF EXISTS LearningPath
CREATE TABLE LearningPath (
  id INT PRIMARY KEY IDENTITY(1,1),
  title TEXT,
  description TEXT,
  mentor_id INT,
  created_at DATETIME,
  updated_at DATETIME,
  FOREIGN KEY (mentor_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS CourseLearningPath
CREATE TABLE CourseLearningPath (
  learning_path_id INT,
  course_id INT,
  FOREIGN KEY (learning_path_id) REFERENCES LearningPath(id),
  FOREIGN KEY (course_id) REFERENCES Course(id)
);

DROP TABLE IF EXISTS LearningPathProgress
CREATE TABLE LearningPathProgress (
  learning_path_id INT,
  mentee_id INT,
  progress FLOAT,
  FOREIGN KEY (learning_path_id) REFERENCES LearningPath(id),
  FOREIGN KEY (mentee_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS MenteeCourse
CREATE TABLE MenteeCourse (
  mentee_id INT,
  course_id INT,
  progress INT,
  enroll_at DATETIME,
  cert_id INT,
  issued_on DATE,
  expiry_at DATE,
  FOREIGN KEY (mentee_id) REFERENCES [User](id),
  FOREIGN KEY (course_id) REFERENCES Course(id)
);

DROP TABLE IF EXISTS FavouriteCategory
CREATE TABLE FavouriteCategory (
  mentee_id INT,
  category_id INT,
  FOREIGN KEY (category_id) REFERENCES Category(id),
  FOREIGN KEY (mentee_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS Setting
CREATE TABLE Setting (
  id INT PRIMARY KEY IDENTITY(1,1),
  setting_type VARCHAR(255),
  setting_name VARCHAR(255),
  setting_value INT
);

DROP TABLE IF EXISTS EventType
CREATE TABLE EventType (
  id INT PRIMARY KEY IDENTITY(1,1),
  event_type_name VARCHAR(255)
);

DROP TABLE IF EXISTS Program
CREATE TABLE Program (
  id INT PRIMARY KEY IDENTITY(1,1),
  user_id INT,
  program_name VARCHAR(255),
  description VARCHAR(255),
  price FLOAT,
  category_id INT,
  asset_id INT,
  FOREIGN KEY (user_id) REFERENCES [User](id),
  FOREIGN KEY (category_id) REFERENCES Category(id)
);

DROP TABLE IF EXISTS ProgramUser
CREATE TABLE ProgramUser (
  program_id INT,
  user_id INT,
  progress_percent FLOAT,
  status VARCHAR(50),
  start_at DATE,
  FOREIGN KEY (program_id) REFERENCES Program(id),
  FOREIGN KEY (user_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS ProgramSource
CREATE TABLE ProgramSource (
  program_id INT ,
  source_id INT,
  source_type_id INT,
  source_order INT,
  FOREIGN KEY (program_id) REFERENCES Program(id)
);

DROP TABLE IF EXISTS ProgramMentor
CREATE TABLE ProgramMentor (
  program_id INT,
  user_id INT,
  FOREIGN KEY (program_id) REFERENCES Program(id),
  FOREIGN KEY (user_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS Challenge
CREATE TABLE Challenge (
  id INT PRIMARY KEY IDENTITY(1,1),
  user_id INT,
  category_id INT,
  challenge_name VARCHAR(255),
  description VARCHAR(255),
  location VARCHAR(255),
  phase VARCHAR(255),
  start_date DATETIME,
  FOREIGN KEY (user_id) REFERENCES [User](id),
  FOREIGN KEY (category_id) REFERENCES Category(id)
);

DROP TABLE IF EXISTS ChallengeUser
CREATE TABLE ChallengeUser (
  challenge_id INT,
  user_id INT,
  score FLOAT,
  status VARCHAR(255),
  date_submission DATETIME,
  FOREIGN KEY (challenge_id) REFERENCES Challenge(id),
  FOREIGN KEY (user_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS FollowUser
CREATE TABLE FollowUser (
  id INT PRIMARY KEY IDENTITY(1,1),
  follower_id INT,
  followee_id INT,
  datefollow DATETIME,
  FOREIGN KEY (follower_id) REFERENCES [User](id),
  FOREIGN KEY (followee_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS SourceTemplate
CREATE TABLE SourceTemplate (
  id INT PRIMARY KEY IDENTITY(1,1),
  template_id INT,
  source_id INT,
  sourcetype_id INT,
  FOREIGN KEY (sourcetype_id) REFERENCES Setting(id)
);

DROP TABLE IF EXISTS CredentialIssued
CREATE TABLE CredentialIssued (
  id INT PRIMARY KEY IDENTITY(1,1),
  sourcetemplate_id INT,
  user_id INT,
  credentialcode VARCHAR(50),
  certified_at DATETIME,
  FOREIGN KEY (sourcetemplate_id) REFERENCES SourceTemplate(id),
  FOREIGN KEY (user_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS Company
CREATE TABLE Company (
  id INT PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255),
  img VARCHAR(255)
);

DROP TABLE IF EXISTS WorkingType
CREATE TABLE WorkingType (
  id INT PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255)
);

DROP TABLE IF EXISTS Experience
CREATE TABLE Experience (
  id INT PRIMARY KEY IDENTITY(1,1),
  jobtitle_id INT,
  company_id INT,
  type_id INT,
  user_id INT,
  isworking BIT,
  FOREIGN KEY (company_id) REFERENCES Company(id),
  FOREIGN KEY (user_id) REFERENCES [User](id),
  FOREIGN KEY (jobtitle_id) REFERENCES Jobtitle(id),
  FOREIGN KEY (type_id) REFERENCES WorkingType(id)
);

DROP TABLE IF EXISTS University
CREATE TABLE University (
  id INT PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255),
  img VARCHAR(255)
);

DROP TABLE IF EXISTS Education
CREATE TABLE Education (
  id INT PRIMARY KEY IDENTITY(1,1),
  degree VARCHAR(255),
  university_id INT,
  user_id INT,
  FOREIGN KEY (university_id) REFERENCES University(id),
  FOREIGN KEY (user_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS Skill
CREATE TABLE Skill (
  id INT PRIMARY KEY IDENTITY(1,1),
  name VARCHAR(255)
);

DROP TABLE IF EXISTS UserSkill
CREATE TABLE UserSkill (
  id INT PRIMARY KEY IDENTITY(1,1),
  user_id INT,
  skill_id INT,
  FOREIGN KEY (user_id) REFERENCES [User](id),
  FOREIGN KEY (skill_id) REFERENCES Skill(id)
);

DROP TABLE IF EXISTS Event
CREATE TABLE Event (
  id INT PRIMARY KEY IDENTITY(1,1),
  title VARCHAR(255),
  user_id INT,
  views INT,
  create_at DATETIME,
  FOREIGN KEY (user_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS EventUser
CREATE TABLE EventUser (
  id INT PRIMARY KEY IDENTITY(1,1),
  event_id INT,
  user_id INT,
  FOREIGN KEY (event_id) REFERENCES Event(id),
  FOREIGN KEY (user_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS MentorReview
CREATE TABLE MentorReview (
  id INT PRIMARY KEY IDENTITY(1,1),
  sender_id INT,
  receiver_id INT,
  rating_star INT,
  content VARCHAR(255),
  FOREIGN KEY (sender_id) REFERENCES [User](id),
  FOREIGN KEY (receiver_id) REFERENCES [User](id)
);

DROP TABLE IF EXISTS [Role];
CREATE TABLE Role
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS Subsystem
CREATE TABLE Subsystem
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255),
    description varchar(500),
    created_at datetime
);

DROP TABLE IF EXISTS NotificationType;
CREATE TABLE NotificationType
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS NotificationType;
CREATE TABLE NotificationType
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS StatusMessage;
CREATE TABLE StatusMessage
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS Workspace;
CREATE TABLE Workspace
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255),
    owner_id int,
    source_id int DEFAULT null,
    source_type_id int
);

DROP TABLE IF EXISTS EventType;
CREATE TABLE EventType
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS MeetingParticipantStatus;
CREATE TABLE MeetingParticipantStatus
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS Channel;
CREATE TABLE Channel
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    workspace_id int,
    name varchar(255),
    description varchar(500),
    is_private tinyInt DEFAULT 1,
    created_at datetime
);

DROP TABLE IF EXISTS [Language];
CREATE TABLE Language
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS MainFeature;
CREATE TABLE MainFeature
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS Emoji;
CREATE TABLE Emoji
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    unicode varchar(255),
    name varchar(255)
);

DROP TABLE IF EXISTS FeedbackGroup;
CREATE TABLE FeedbackGroup
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS FeedbackStatus;
CREATE TABLE FeedbackStatus
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255)
);

DROP TABLE IF EXISTS Meeting;
CREATE TABLE Meeting
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    owner_id int,
    name varchar(255),
    description varchar(500),
    start_at datetime,
    end_at datetime,
    created_at datetime
);

DROP TABLE IF EXISTS DirectMessage;
CREATE TABLE DirectMessage
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    user1 int,
    user2 int,
    created_at datetime
);

DROP TABLE IF EXISTS MeetingParticipant;
CREATE TABLE MeetingParticipant
(
    meeting_id int,
    user_id int,
    status_id int,
    joined_at datetime DEFAULT null,
    left_at datetime DEFAULT null
);

DROP TABLE IF EXISTS NotificationQueue;
CREATE TABLE NotificationQueue
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    user_id int,
    notification_type_id int,
    content text,
    is_read tinyInt DEFAULT 0
);

DROP TABLE IF EXISTS Permission;
CREATE TABLE Permission
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,

    role_id int,
    name varchar(255),
    value int
);

DROP TABLE IF EXISTS WorkspaceMember;
CREATE TABLE WorkspaceMember
(
    workspace_id int,
    user_id int,
    join_at datetime,
    updated_at datetime,
    left_at datetime DEFAULT null,
    role_id int DEFAULT null
);

DROP TABLE IF EXISTS ChannelShared;
CREATE TABLE ChannelShared
(
    channel_id int,
    original_workspace_id int,
    target_workspace_id int
);

DROP TABLE IF EXISTS PollQuestion;
CREATE TABLE PollQuestion
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    question varchar(255),
    channel_id int,
    created_by int,
    created_at datetime,
    expires_at datetime
);

DROP TABLE IF EXISTS PollAnswer;
CREATE TABLE PollAnswer
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    question_id int,
    answer varchar(255),
    created_by int,
    created_at datetime
);

DROP TABLE IF EXISTS PollVotingHistory;
CREATE TABLE PollVotingHistory
(
    question_id int,
    answer_id int,
    voted_by int,
    voted_at datetime
);

DROP TABLE IF EXISTS [Log];
CREATE TABLE Log
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    user_id int,
    event_type_id int,
    log_time datetime
);

DROP TABLE IF EXISTS EventParameter;
CREATE TABLE EventParameter
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    name varchar(255),
    data_type varchar(255),
    event_type_id int
);

DROP TABLE IF EXISTS LogDetail;
CREATE TABLE LogDetail
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    log_id int,
    event_parameter_id int,
    value varchar(255)
);

DROP TABLE IF EXISTS ChannelPrivateMember;
CREATE TABLE ChannelPrivateMember
(
    channel_id int,
    user_id int,
    role_id int DEFAULT null
);

DROP TABLE IF EXISTS [Message];
CREATE TABLE [Message]
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,

    sender_id int,
    content text,
    channel_id int DEFAULT null,
    dms_id int DEFAULT null,
    parent_id int DEFAULT null,
    meeting_id int DEFAULT null,
    status_id int DEFAULT null,
    send_at datetime,
    edited_at datetime DEFAULT null,
    is_deleted tinyInt DEFAULT 0,
    deleted_at datetime DEFAULT null
);

DROP TABLE IF EXISTS MessageMention;
CREATE TABLE MessageMention
(
    message_id int,
    user_id int
);

DROP TABLE IF EXISTS MessageAttachment;
CREATE TABLE MessageAttachment
(
    message_id int,
    asset_id int
);

DROP TABLE IF EXISTS MessageReaction;
CREATE TABLE MessageReaction
(
    message_id int,
    emoji_id int,
    user_id int
);

DROP TABLE IF EXISTS BlockList;
CREATE TABLE BlockList
(
    user_id int,
    user_id_is_blocked int,
    dms_id int
);

DROP TABLE IF EXISTS Feedback;
CREATE TABLE Feedback
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    user_id int,
    subsystem_id int,
    sender_email varchar(100),
    group_id int DEFAULT null,
    status_id int,
    content text,
    send_at datetime,
    updated_at datetime DEFAULT null
);

DROP TABLE IF EXISTS FeedbackAttachment
CREATE TABLE FeedbackAttachment
(
    feedback_id int,
    asset_id int
);
	
DROP TABLE IF EXISTS FeedbackAssignee;
CREATE TABLE FeedbackAssignee
(
    feedback_id int,
    assignee_id int,
    assign_at datetime,
    content text
);
DROP TABLE IF EXISTS FeedbackResult;
CREATE TABLE FeedbackResult
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    feedback_id int,
    content text,
    send_at datetime
);

DROP TABLE IF EXISTS NavigationBar;
CREATE TABLE NavigationBar
(
    user_id int,
    feature_nav_bar int
);

DROP TABLE IF EXISTS NotificationSetting;
CREATE TABLE NotificationSetting
(
    preference_id int,
    notification_type_id int,
    enable tinyInt DEFAULT 1
);

DROP TABLE IF EXISTS Preference;
CREATE TABLE Preference
(
    id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
    user_id int,
    dark_mode tinyInt DEFAULT 0,
    language_id int
);

DROP TABLE IF EXISTS FeedbackResultReply;
CREATE TABLE FeedbackResultReply
(
    feedback_result_id int,
    replied_by int,
    replied_at datetime,
    content text
);

ALTER TABLE Workspace ADD FOREIGN KEY (owner_id) REFERENCES [User] (id);

ALTER TABLE Channel ADD FOREIGN KEY (workspace_id) REFERENCES Workspace (id);

ALTER TABLE Meeting ADD FOREIGN KEY (owner_id) REFERENCES [User] (id);

ALTER TABLE DirectMessage ADD FOREIGN KEY (user1) REFERENCES [User] (id);

ALTER TABLE DirectMessage ADD FOREIGN KEY (user2) REFERENCES [User] (id);

ALTER TABLE MeetingParticipant ADD FOREIGN KEY (meeting_id) REFERENCES Meeting (id);

ALTER TABLE MeetingParticipant ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE MeetingParticipant ADD FOREIGN KEY (status_id) REFERENCES MeetingParticipantStatus (id);

ALTER TABLE NotificationQueue ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE NotificationQueue ADD FOREIGN KEY (notification_type_id) REFERENCES NotificationType (id);

ALTER TABLE Permission ADD FOREIGN KEY (role_id) REFERENCES role (id);

ALTER TABLE WorkspaceMember ADD FOREIGN KEY (workspace_id) REFERENCES Workspace (id);

ALTER TABLE WorkspaceMember ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE WorkspaceMember ADD FOREIGN KEY (role_id) REFERENCES role (id);

ALTER TABLE ChannelShared ADD FOREIGN KEY (channel_id) REFERENCES Channel (id);

ALTER TABLE ChannelShared ADD FOREIGN KEY (original_workspace_id) REFERENCES Workspace (id);

ALTER TABLE ChannelShared ADD FOREIGN KEY (target_workspace_id) REFERENCES Workspace (id);

ALTER TABLE PollQuestion ADD FOREIGN KEY (channel_id) REFERENCES Channel (id);

ALTER TABLE PollQuestion ADD FOREIGN KEY (created_by) REFERENCES [User] (id);

ALTER TABLE PollAnswer ADD FOREIGN KEY (question_id) REFERENCES PollQuestion (id);

ALTER TABLE PollAnswer ADD FOREIGN KEY (created_by) REFERENCES [User] (id);

ALTER TABLE PollVotingHistory ADD FOREIGN KEY (question_id) REFERENCES PollQuestion (id);

ALTER TABLE PollVotingHistory ADD FOREIGN KEY (answer_id) REFERENCES PollAnswer (id);

ALTER TABLE PollVotingHistory ADD FOREIGN KEY (voted_by) REFERENCES [User] (id);

ALTER TABLE log ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE log ADD FOREIGN KEY (event_type_id) REFERENCES EventType (id);

ALTER TABLE EventParameter ADD FOREIGN KEY (event_type_id) REFERENCES EventType (id);

ALTER TABLE LogDetail ADD FOREIGN KEY (log_id) REFERENCES log (id);

ALTER TABLE LogDetail ADD FOREIGN KEY (event_parameter_id) REFERENCES EventParameter (id);

ALTER TABLE ChannelPrivateMember ADD FOREIGN KEY (channel_id) REFERENCES Channel (id);

ALTER TABLE ChannelPrivateMember ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE ChannelPrivateMember ADD FOREIGN KEY (role_id) REFERENCES role (id);

ALTER TABLE [Message] ADD FOREIGN KEY (sender_id) REFERENCES [User] (id);

ALTER TABLE [Message] ADD FOREIGN KEY (channel_id) REFERENCES Channel (id);

ALTER TABLE [Message] ADD FOREIGN KEY (dms_id) REFERENCES DirectMessage (id);

ALTER TABLE [Message] ADD FOREIGN KEY (parent_id) REFERENCES [Message] (id);

ALTER TABLE [Message] ADD FOREIGN KEY (meeting_id) REFERENCES Meeting (id);

ALTER TABLE [Message] ADD FOREIGN KEY (status_id) REFERENCES StatusMessage(id);

ALTER TABLE MessageMention ADD FOREIGN KEY (message_id) REFERENCES [Message] (id);

ALTER TABLE MessageMention ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE MessageAttachment ADD FOREIGN KEY (message_id) REFERENCES [Message] (id);

ALTER TABLE MessageReaction ADD FOREIGN KEY (message_id) REFERENCES [Message] (id);

ALTER TABLE MessageReaction ADD FOREIGN KEY (emoji_id) REFERENCES Emoji (id);

ALTER TABLE MessageReaction ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE BlockList ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE BlockList ADD FOREIGN KEY (user_id_is_blocked) REFERENCES [User] (id);

ALTER TABLE BlockList ADD FOREIGN KEY (dms_id) REFERENCES DirectMessage (id);

ALTER TABLE Feedback ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE Feedback ADD FOREIGN KEY (subsystem_id) REFERENCES Subsystem (id);

ALTER TABLE Feedback ADD FOREIGN KEY (group_id) REFERENCES FeedbackGroup (id);

ALTER TABLE Feedback ADD FOREIGN KEY (status_id) REFERENCES FeedbackStatus (id);

ALTER TABLE FeedbackAssignee ADD FOREIGN KEY (feedback_id) REFERENCES Feedback (id);

ALTER TABLE FeedbackAssignee ADD FOREIGN KEY (assignee_id) REFERENCES [User] (id);

ALTER TABLE FeedbackResult ADD FOREIGN KEY (feedback_id) REFERENCES Feedback (id);

ALTER TABLE FeedbackResultReply ADD FOREIGN KEY (feedback_result_id) REFERENCES FeedbackResult (id);

ALTER TABLE FeedbackResultReply ADD FOREIGN KEY (replied_by) REFERENCES [User] (id);

ALTER TABLE NavigationBar ADD FOREIGN KEY (user_id) REFERENCES [User] (id);

ALTER TABLE NavigationBar ADD FOREIGN KEY (feature_nav_bar) REFERENCES MainFeature (id);

ALTER TABLE NotificationSetting ADD FOREIGN KEY (preference_id) REFERENCES Preference (id);

ALTER TABLE NotificationSetting ADD FOREIGN KEY (notification_type_id) REFERENCES NotificationType (id);

ALTER TABLE Preference ADD FOREIGN KEY (language_id) REFERENCES language (id);

```