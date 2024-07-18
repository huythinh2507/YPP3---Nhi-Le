```sql
USE [MentorHub]
GO
/****** Object:  Table [dbo].[Setting]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Setting](
	[id] [int] NOT NULL,
	[setting_type] [varchar](255) NULL,
	[setting_name] [varchar](255) NULL,
	[setting_value] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  UserDefinedFunction [dbo].[GetSettingValue]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE FUNCTION [dbo].[GetSettingValue]
(
    @category varchar(255),
	@variable varchar(255)
)
RETURNS TABLE
AS
RETURN
(
    SELECT
		setting_value
    FROM
        Setting
    WHERE 
        setting_type = @category and setting_name = @variable
);
GO
/****** Object:  Table [dbo].[Ads]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Ads](
	[source_id] [int] IDENTITY(1,1) NOT NULL,
	[source_type] [int] NULL,
	[thumbnail_id] [int] NULL,
	[start_at] [datetime] NULL,
	[end_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[source_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Answer]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Answer](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[question_id] [int] NULL,
	[content] [text] NULL,
	[asset_id] [int] NULL,
	[is_correct] [bit] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[BlockList]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[BlockList](
	[user_id] [int] NULL,
	[user_id_is_blocked] [int] NULL,
	[dms_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[CartItem]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[CartItem](
	[id] [int] NOT NULL,
	[user_id] [int] NULL,
	[source_id] [int] NULL,
	[source_type_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Category]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Category](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Challenge]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Challenge](
	[id] [int] NOT NULL,
	[user_id] [int] NULL,
	[category_id] [int] NULL,
	[challenge_name] [varchar](255) NULL,
	[description] [varchar](255) NULL,
	[location] [varchar](255) NULL,
	[phase] [varchar](255) NULL,
	[start_date] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[ChallengeUser]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[ChallengeUser](
	[challenge_id] [int] NULL,
	[user_id] [int] NULL,
	[score] [float] NULL,
	[status] [varchar](255) NULL,
	[date_submission] [datetime] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Channel]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Channel](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[workspace_id] [int] NULL,
	[name] [varchar](255) NULL,
	[description] [varchar](500) NULL,
	[is_private] [tinyint] NULL,
	[created_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[ChannelPrivateMember]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[ChannelPrivateMember](
	[channel_id] [int] NULL,
	[user_id] [int] NULL,
	[role_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[ChannelShared]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[ChannelShared](
	[channel_id] [int] NULL,
	[original_workspace_id] [int] NULL,
	[target_workspace_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Company]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Company](
	[id] [int] NOT NULL,
	[name] [varchar](255) NULL,
	[img] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Course]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Course](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [nvarchar](255) NULL,
	[category_id] [int] NULL,
	[price] [decimal](10, 2) NULL,
	[description] [text] NULL,
	[created_at] [datetime] NULL,
	[mentor_id] [int] NULL,
	[pass_condition] [int] NULL,
	[thumbnail_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[CourseLearningPath]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[CourseLearningPath](
	[learning_path_id] [int] NULL,
	[course_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[CredentialIssued]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[CredentialIssued](
	[id] [int] NOT NULL,
	[sourcetemplate_id] [int] NULL,
	[user_id] [int] NULL,
	[credentialcode] [varchar](50) NULL,
	[certified_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[DirectMessage]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[DirectMessage](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[user1] [int] NULL,
	[user2] [int] NULL,
	[created_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Discussion]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Discussion](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[user_id] [int] NULL,
	[lesson_id] [int] NULL,
	[parent_discussion_id] [int] NULL,
	[content] [text] NULL,
	[created_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Education]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Education](
	[id] [int] NOT NULL,
	[degree] [varchar](255) NULL,
	[university_id] [int] NULL,
	[user_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Emoji]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Emoji](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[unicode] [varchar](255) NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Event]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Event](
	[id] [int] NOT NULL,
	[title] [varchar](255) NULL,
	[user_id] [int] NULL,
	[views] [int] NULL,
	[create_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[EventLog]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[EventLog](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[user_id] [int] NULL,
	[source_id] [int] NULL,
	[source_type_id] [int] NULL,
	[event_type_id] [int] NULL,
	[event_time] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[EventParameter]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[EventParameter](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
	[data_type] [varchar](255) NULL,
	[event_type_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[EventType]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[EventType](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[event_type_name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[EventTypeMess]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[EventTypeMess](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[EventUser]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[EventUser](
	[id] [int] NOT NULL,
	[event_id] [int] NULL,
	[user_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Experience]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Experience](
	[id] [int] NOT NULL,
	[jobtitle_id] [int] NULL,
	[company_id] [int] NULL,
	[type_id] [int] NULL,
	[user_id] [int] NULL,
	[isworking] [bit] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[FavouriteCategory]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[FavouriteCategory](
	[mentee_id] [int] NULL,
	[category_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Feedback]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Feedback](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[user_id] [int] NULL,
	[subsystem_id] [int] NULL,
	[sender_email] [varchar](100) NULL,
	[group_id] [int] NULL,
	[status_id] [int] NULL,
	[content] [text] NULL,
	[send_at] [datetime] NULL,
	[updated_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[FeedbackAssignee]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[FeedbackAssignee](
	[feedback_id] [int] NULL,
	[assignee_id] [int] NULL,
	[assign_at] [datetime] NULL,
	[content] [text] NULL
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[FeedbackAttachment]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[FeedbackAttachment](
	[feedback_id] [int] NULL,
	[asset_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[FeedbackGroup]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[FeedbackGroup](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[FeedbackResult]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[FeedbackResult](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[feedback_id] [int] NULL,
	[content] [text] NULL,
	[send_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[FeedbackResultReply]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[FeedbackResultReply](
	[feedback_result_id] [int] NULL,
	[replied_by] [int] NULL,
	[replied_at] [datetime] NULL,
	[content] [text] NULL
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[FeedbackStatus]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[FeedbackStatus](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[FollowUser]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[FollowUser](
	[id] [int] NOT NULL,
	[follower_id] [int] NULL,
	[followee_id] [int] NULL,
	[datefollow] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Jobtitle]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Jobtitle](
	[id] [int] NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Language]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Language](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[LearningPath]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[LearningPath](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[title] [text] NULL,
	[description] [text] NULL,
	[mentor_id] [int] NULL,
	[created_at] [datetime] NULL,
	[updated_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[LearningPathProgress]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[LearningPathProgress](
	[learning_path_id] [int] NULL,
	[mentee_id] [int] NULL,
	[progress] [float] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Lesson]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Lesson](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[section_id] [int] NULL,
	[title] [varchar](255) NULL,
	[transcript] [text] NULL,
	[summary] [text] NULL,
	[asset_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Location]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Location](
	[id] [int] NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Log]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Log](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[user_id] [int] NULL,
	[event_type_id] [int] NULL,
	[log_time] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[LogDetail]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[LogDetail](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[log_id] [int] NULL,
	[event_parameter_id] [int] NULL,
	[value] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MainFeature]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MainFeature](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Meeting]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Meeting](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[owner_id] [int] NULL,
	[name] [varchar](255) NULL,
	[description] [varchar](500) NULL,
	[start_at] [datetime] NULL,
	[end_at] [datetime] NULL,
	[created_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MeetingParticipant]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MeetingParticipant](
	[meeting_id] [int] NULL,
	[user_id] [int] NULL,
	[status_id] [int] NULL,
	[joined_at] [datetime] NULL,
	[left_at] [datetime] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MeetingParticipantStatus]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MeetingParticipantStatus](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MemberActiveCount]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MemberActiveCount](
	[day] [date] NULL,
	[active_count] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MenteeCourse]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MenteeCourse](
	[mentee_id] [int] NULL,
	[course_id] [int] NULL,
	[progress] [int] NULL,
	[enroll_at] [datetime] NULL,
	[cert_id] [int] NULL,
	[issued_on] [date] NULL,
	[expiry_at] [date] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MenteeQuestion]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MenteeQuestion](
	[mentee_id] [int] NULL,
	[question_id] [int] NULL,
	[earned_marks] [float] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MenteeSaveCourse]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MenteeSaveCourse](
	[course_id] [int] NULL,
	[mentee_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MentorReview]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MentorReview](
	[id] [int] NOT NULL,
	[sender_id] [int] NULL,
	[receiver_id] [int] NULL,
	[rating_star] [int] NULL,
	[content] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Message]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Message](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[sender_id] [int] NULL,
	[content] [text] NULL,
	[channel_id] [int] NULL,
	[dms_id] [int] NULL,
	[parent_id] [int] NULL,
	[meeting_id] [int] NULL,
	[status_id] [int] NULL,
	[send_at] [datetime] NULL,
	[edited_at] [datetime] NULL,
	[is_deleted] [tinyint] NULL,
	[deleted_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MessageAttachment]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MessageAttachment](
	[message_id] [int] NULL,
	[asset_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MessageMention]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MessageMention](
	[message_id] [int] NULL,
	[user_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[MessageReaction]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[MessageReaction](
	[message_id] [int] NULL,
	[emoji_id] [int] NULL,
	[user_id] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[NavigationBar]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[NavigationBar](
	[user_id] [int] NULL,
	[feature_nav_bar] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[NotificationQueue]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[NotificationQueue](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[user_id] [int] NULL,
	[notification_type_id] [int] NULL,
	[content] [text] NULL,
	[is_read] [tinyint] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[NotificationSetting]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[NotificationSetting](
	[preference_id] [int] NULL,
	[notification_type_id] [int] NULL,
	[enable] [tinyint] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[NotificationType]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[NotificationType](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Order]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Order](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[user_id] [int] NULL,
	[user_payment_id] [int] NULL,
	[status] [int] NULL,
	[created_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[OrderDetail]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[OrderDetail](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[order_id] [int] NULL,
	[price] [decimal](10, 2) NULL,
	[source_id] [int] NULL,
	[source_type_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[PaymentMethod]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[PaymentMethod](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[method] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Permission]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Permission](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[role_id] [int] NULL,
	[name] [varchar](255) NULL,
	[value] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[PollAnswer]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[PollAnswer](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[question_id] [int] NULL,
	[answer] [varchar](255) NULL,
	[created_by] [int] NULL,
	[created_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[PollQuestion]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[PollQuestion](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[question] [varchar](255) NULL,
	[channel_id] [int] NULL,
	[created_by] [int] NULL,
	[created_at] [datetime] NULL,
	[expires_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[PollVotingHistory]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[PollVotingHistory](
	[question_id] [int] NULL,
	[answer_id] [int] NULL,
	[voted_by] [int] NULL,
	[voted_at] [datetime] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Preference]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Preference](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[user_id] [int] NULL,
	[dark_mode] [tinyint] NULL,
	[language_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Program]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Program](
	[id] [int] NOT NULL,
	[user_id] [int] NULL,
	[program_name] [varchar](255) NULL,
	[description] [varchar](255) NULL,
	[price] [float] NULL,
	[category_id] [int] NULL,
	[asset_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[ProgramMentor]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[ProgramMentor](
	[program_id] [int] NOT NULL,
	[user_id] [int] NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[program_id] ASC,
	[user_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[ProgramSource]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[ProgramSource](
	[program_id] [int] NOT NULL,
	[source_id] [int] NOT NULL,
	[source_type_id] [int] NOT NULL,
	[source_order] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[program_id] ASC,
	[source_id] ASC,
	[source_type_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[ProgramUser]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[ProgramUser](
	[program_id] [int] NOT NULL,
	[user_id] [int] NOT NULL,
	[progress_percent] [float] NULL,
	[status] [varchar](50) NULL,
	[start_at] [date] NULL,
PRIMARY KEY CLUSTERED 
(
	[program_id] ASC,
	[user_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Progress]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Progress](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[lesson_id] [int] NULL,
	[mentee_id] [int] NULL,
	[course_id] [int] NULL,
	[time_closed] [datetime] NULL,
	[status] [bit] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Question]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Question](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[question_type_id] [int] NULL,
	[quiz_id] [int] NULL,
	[title] [text] NULL,
	[randomize] [bit] NULL,
	[points] [float] NULL,
	[explanation] [text] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[QuestionType]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[QuestionType](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[type] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Quiz]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Quiz](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
	[summary] [text] NULL,
	[attempts_allowed] [int] NULL,
	[passing_grade] [int] NULL,
	[duration] [time](7) NULL,
	[section_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[QuizResult]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[QuizResult](
	[mentee_id] [int] NULL,
	[quiz_id] [int] NULL,
	[date] [datetime] NULL,
	[mark] [float] NULL,
	[result] [bit] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Resource]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Resource](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[asset_id] [int] NULL,
	[lesson_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Review]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Review](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[source_id] [int] NULL,
	[user_id] [int] NULL,
	[source_type_id] [int] NULL,
	[rating_star] [int] NULL,
	[content] [varchar](255) NULL,
	[review_at] [time](7) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Role]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Role](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](50) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Section]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Section](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
	[course_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Skill]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Skill](
	[id] [int] NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[SourceImage]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[SourceImage](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[source_id] [int] NULL,
	[asset_id] [int] NULL,
	[source_type_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[SourceTag]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[SourceTag](
	[source_id] [int] NOT NULL,
	[source_type_id] [int] NOT NULL,
	[tag_id] [int] NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[source_id] ASC,
	[source_type_id] ASC,
	[tag_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[SourceTemplate]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[SourceTemplate](
	[id] [int] NOT NULL,
	[template_id] [int] NULL,
	[source_id] [int] NULL,
	[sourcetype_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[StatusMessage]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[StatusMessage](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Subsystem]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Subsystem](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
	[description] [varchar](500) NULL,
	[created_at] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Tag]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Tag](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[tag_name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[TotalMember]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[TotalMember](
	[total_member] [int] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[University]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[University](
	[id] [int] NOT NULL,
	[name] [varchar](255) NULL,
	[img] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[User]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[User](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
	[asset_id] [int] NULL,
	[location_id] [int] NULL,
	[jobtitle_id] [int] NULL,
	[role_id] [int] NULL,
	[create_at] [datetime] NULL,
	[age] [int] NULL,
	[gender] [varchar](10) NULL,
	[status] [bit] NULL,
	[dob] [date] NULL,
	[email] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[UserOnline]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[UserOnline](
	[user_id] [int] NULL,
	[online_date] [date] NULL,
	[online_time] [time](7) NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[UserPaymentInfo]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[UserPaymentInfo](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[user_id] [int] NULL,
	[name_on_card] [varchar](255) NULL,
	[card_number] [varchar](20) NULL,
	[expiry_date] [datetime] NULL,
	[payment_method_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[UserSkill]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[UserSkill](
	[id] [int] NOT NULL,
	[user_id] [int] NULL,
	[skill_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Voucher]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Voucher](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[code] [varchar](255) NULL,
	[source_id] [int] NULL,
	[source_type_id] [int] NULL,
	[discount] [float] NULL,
	[quantity] [int] NULL,
	[expire_date] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[WorkingType]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[WorkingType](
	[id] [int] NOT NULL,
	[name] [varchar](255) NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Workspace]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Workspace](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[name] [varchar](255) NULL,
	[owner_id] [int] NULL,
	[source_id] [int] NULL,
	[source_type_id] [int] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[WorkspaceMember]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[WorkspaceMember](
	[workspace_id] [int] NULL,
	[user_id] [int] NULL,
	[join_at] [datetime] NULL,
	[updated_at] [datetime] NULL,
	[left_at] [datetime] NULL,
	[role_id] [int] NULL
) ON [PRIMARY]
GO
SET IDENTITY_INSERT [dbo].[Ads] ON 

INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (1, 1, 1, CAST(N'2023-01-01T08:00:00.000' AS DateTime), CAST(N'2023-01-31T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (2, 2, 2, CAST(N'2023-02-01T08:00:00.000' AS DateTime), CAST(N'2023-02-28T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (3, 3, 3, CAST(N'2023-03-01T08:00:00.000' AS DateTime), CAST(N'2023-03-31T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (4, 1, 4, CAST(N'2023-04-01T08:00:00.000' AS DateTime), CAST(N'2023-04-30T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (5, 2, 5, CAST(N'2023-05-01T08:00:00.000' AS DateTime), CAST(N'2023-05-31T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (6, 3, 6, CAST(N'2023-06-01T08:00:00.000' AS DateTime), CAST(N'2023-06-30T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (7, 1, 7, CAST(N'2023-07-01T08:00:00.000' AS DateTime), CAST(N'2023-07-31T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (8, 2, 8, CAST(N'2023-08-01T08:00:00.000' AS DateTime), CAST(N'2023-08-31T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (9, 3, 9, CAST(N'2023-09-01T08:00:00.000' AS DateTime), CAST(N'2023-09-30T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (10, 1, 10, CAST(N'2023-10-01T08:00:00.000' AS DateTime), CAST(N'2023-10-31T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (11, 2, 1, CAST(N'2023-11-01T08:00:00.000' AS DateTime), CAST(N'2023-11-30T23:59:59.000' AS DateTime))
INSERT [dbo].[Ads] ([source_id], [source_type], [thumbnail_id], [start_at], [end_at]) VALUES (12, 3, 2, CAST(N'2023-12-01T08:00:00.000' AS DateTime), CAST(N'2023-12-31T23:59:59.000' AS DateTime))
SET IDENTITY_INSERT [dbo].[Ads] OFF
GO
SET IDENTITY_INSERT [dbo].[Answer] ON 

INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (1, 1, N'Information Technology is the use of computers to store, retrieve, transmit, and manipulate data.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (2, 2, N'Computers, smartphones, servers', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (3, 2, N'Refrigerators, microwaves, toasters', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (4, 3, N'User Interface', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (5, 3, N'User Interaction', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (6, 4, N'UI is the look and feel, UX is the experience.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (7, 4, N'UI is the experience, UX is the look and feel.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (8, 5, N'Marketing is the process of promoting and selling products or services.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (9, 5, N'Marketing is the process of producing goods.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (10, 6, N'Product, Price, Place, Promotion', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (11, 6, N'Production, People, Planning, Promotion', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (12, 7, N'A healthy lifestyle helps maintain physical and mental health.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (13, 7, N'A healthy lifestyle helps in earning more money.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (14, 8, N'Improved fitness, enhanced mood', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (15, 8, N'Better financial status, increased sleep', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (16, 9, N'Aperture controls the amount of light entering the camera.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (17, 9, N'Aperture adjusts the focus of the lens.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (18, 10, N'Rule of thirds is a composition technique for balancing images.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (19, 10, N'Rule of thirds is a lighting technique.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (20, 11, N'Video editing involves rearranging video shots to create a new work.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (21, 11, N'Video editing is about recording video.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (22, 12, N'Adobe Premiere Pro, Final Cut Pro', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (23, 12, N'Microsoft Word, Excel', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (24, 13, N'Cloud computing is delivering computing services over the internet.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (25, 13, N'Cloud computing is a type of physical storage device.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (26, 14, N'Scalability, Security risks', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (27, 14, N'Cheap cost, No disadvantages', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (28, 15, N'A wireframe is a basic visual guide to suggest the structure of an interface.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (29, 15, N'A wireframe is a final design of an interface.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (30, 16, N'User personas are fictional characters created to represent different user types.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (31, 16, N'User personas are real users interacting with the product.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (32, 17, N'A marketing funnel is a model describing the customer journey.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (33, 17, N'A marketing funnel is a tool for data analysis.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (34, 18, N'Awareness, Interest, Decision, Action', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (35, 18, N'Awareness, Interest, Decision, Purchase', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (36, 19, N'Proper nutrition is essential for maintaining good health.', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (37, 19, N'Proper nutrition is only necessary for athletes.', NULL, 0)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (38, 20, N'Proteins for growth and repair, Carbohydrates for energy', NULL, 1)
INSERT [dbo].[Answer] ([id], [question_id], [content], [asset_id], [is_correct]) VALUES (39, 20, N'Vitamins for energy, Carbohydrates for muscle building', NULL, 0)
SET IDENTITY_INSERT [dbo].[Answer] OFF
GO
INSERT [dbo].[BlockList] ([user_id], [user_id_is_blocked], [dms_id]) VALUES (1, 2, 1)
INSERT [dbo].[BlockList] ([user_id], [user_id_is_blocked], [dms_id]) VALUES (1, 3, 1)
INSERT [dbo].[BlockList] ([user_id], [user_id_is_blocked], [dms_id]) VALUES (2, 3, 1)
INSERT [dbo].[BlockList] ([user_id], [user_id_is_blocked], [dms_id]) VALUES (2, 4, 1)
GO
INSERT [dbo].[CartItem] ([id], [user_id], [source_id], [source_type_id]) VALUES (1, 7, 1, 3)
INSERT [dbo].[CartItem] ([id], [user_id], [source_id], [source_type_id]) VALUES (2, 7, 2, 3)
INSERT [dbo].[CartItem] ([id], [user_id], [source_id], [source_type_id]) VALUES (3, 7, 2, 3)
INSERT [dbo].[CartItem] ([id], [user_id], [source_id], [source_type_id]) VALUES (4, 8, 4, 3)
INSERT [dbo].[CartItem] ([id], [user_id], [source_id], [source_type_id]) VALUES (5, 8, 5, 3)
INSERT [dbo].[CartItem] ([id], [user_id], [source_id], [source_type_id]) VALUES (6, 9, 1, 3)
INSERT [dbo].[CartItem] ([id], [user_id], [source_id], [source_type_id]) VALUES (7, 9, 2, 3)
INSERT [dbo].[CartItem] ([id], [user_id], [source_id], [source_type_id]) VALUES (8, 14, 5, 3)
GO
SET IDENTITY_INSERT [dbo].[Category] ON 

INSERT [dbo].[Category] ([id], [name]) VALUES (1, N'Information Technology')
INSERT [dbo].[Category] ([id], [name]) VALUES (2, N'UI/UX Design')
INSERT [dbo].[Category] ([id], [name]) VALUES (3, N'Marketing')
INSERT [dbo].[Category] ([id], [name]) VALUES (4, N'Lifestyle')
INSERT [dbo].[Category] ([id], [name]) VALUES (5, N'Photography')
INSERT [dbo].[Category] ([id], [name]) VALUES (6, N'Video')
SET IDENTITY_INSERT [dbo].[Category] OFF
GO
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (1, 1, 1, N'Image Classification', N'The challenge is to develop a deep learning model', N'Remote', N'Starting Phase', CAST(N'2024-06-26T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (2, 2, 1, N'Fraud Detection Kaggle', N'Participate in a Kaggle competition', N'HCM', N'Starting Phase', CAST(N'2024-06-27T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (3, 3, 5, N'Short Story Writing', N'Writing a compelling short story', N'Remote', N'Starting Phase', CAST(N'2024-06-23T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (4, 1, 1, N'Data Prediction', N'Predicting data trends using ML', N'Remote', N'Ending Phase', CAST(N'2024-06-27T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (5, 2, 5, N'Recipe Development', N'Creating new and innovative recipes', N'Remote', N'Ending Phase', CAST(N'2024-06-23T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (6, 1, 1, N'E-commerce Website', N'Develop a full-stack e-commerce website', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (7, 2, 1, N'Sentiment Analysis', N'Analyze sentiment from social media data', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (8, 3, 2, N'Mobile App Design', N'Design a mobile app for a retail store', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (9, 3, 3, N'Email Marketing Campaign', N'Create an effective email marketing campaign', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (10, 2, 4, N'Personal Finance Blog', N'Write blog posts about personal finance', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (11, 5, 5, N'Food Photography', N'Capture high-quality photos of food dishes', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (12, 1, 6, N'Short Film Editing', N'Edit a short film with provided footage', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (13, 2, 1, N'Real-time Chat Application', N'Build a real-time chat application', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (14, 3, 2, N'Landing Page Optimization', N'Optimize the landing page of a website', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
INSERT [dbo].[Challenge] ([id], [user_id], [category_id], [challenge_name], [description], [location], [phase], [start_date]) VALUES (15, 6, 5, N'Travel Vlog', N'Create a travel vlog with provided footage', N'Remote', N'Starting Phase', CAST(N'2024-07-01T00:00:00.000' AS DateTime))
GO
INSERT [dbo].[ChallengeUser] ([challenge_id], [user_id], [score], [status], [date_submission]) VALUES (1, 1, 8, N'Passed', CAST(N'2024-06-10T00:00:00.000' AS DateTime))
INSERT [dbo].[ChallengeUser] ([challenge_id], [user_id], [score], [status], [date_submission]) VALUES (2, 1, 6, N'Passed', CAST(N'2024-05-08T00:00:00.000' AS DateTime))
INSERT [dbo].[ChallengeUser] ([challenge_id], [user_id], [score], [status], [date_submission]) VALUES (3, 2, 7, N'Passed', CAST(N'2024-01-23T00:00:00.000' AS DateTime))
INSERT [dbo].[ChallengeUser] ([challenge_id], [user_id], [score], [status], [date_submission]) VALUES (4, 2, 3, N'Failed', CAST(N'2024-02-04T00:00:00.000' AS DateTime))
INSERT [dbo].[ChallengeUser] ([challenge_id], [user_id], [score], [status], [date_submission]) VALUES (5, 3, 5, N'Passed', CAST(N'2024-08-14T00:00:00.000' AS DateTime))
INSERT [dbo].[ChallengeUser] ([challenge_id], [user_id], [score], [status], [date_submission]) VALUES (3, 3, 4, N'Failed', CAST(N'2024-12-17T00:00:00.000' AS DateTime))
GO
SET IDENTITY_INSERT [dbo].[Channel] ON 

INSERT [dbo].[Channel] ([id], [workspace_id], [name], [description], [is_private], [created_at]) VALUES (1, 1, N'Channel 1', N'Description 1', 0, CAST(N'2024-07-18T06:05:13.800' AS DateTime))
INSERT [dbo].[Channel] ([id], [workspace_id], [name], [description], [is_private], [created_at]) VALUES (2, 1, N'Channel 2', N'Description 2', 1, CAST(N'2024-07-18T06:05:13.800' AS DateTime))
INSERT [dbo].[Channel] ([id], [workspace_id], [name], [description], [is_private], [created_at]) VALUES (3, 2, N'Channel 3', N'Description 3', 0, CAST(N'2024-07-18T06:05:13.800' AS DateTime))
INSERT [dbo].[Channel] ([id], [workspace_id], [name], [description], [is_private], [created_at]) VALUES (4, 2, N'Channel 4', N'Description 4', 1, CAST(N'2024-07-18T06:05:13.800' AS DateTime))
SET IDENTITY_INSERT [dbo].[Channel] OFF
GO
INSERT [dbo].[ChannelShared] ([channel_id], [original_workspace_id], [target_workspace_id]) VALUES (1, 1, 2)
INSERT [dbo].[ChannelShared] ([channel_id], [original_workspace_id], [target_workspace_id]) VALUES (2, 1, 2)
INSERT [dbo].[ChannelShared] ([channel_id], [original_workspace_id], [target_workspace_id]) VALUES (3, 2, 1)
INSERT [dbo].[ChannelShared] ([channel_id], [original_workspace_id], [target_workspace_id]) VALUES (4, 2, 1)
GO
INSERT [dbo].[Company] ([id], [name], [img]) VALUES (1, N'bbv', N'link')
INSERT [dbo].[Company] ([id], [name], [img]) VALUES (2, N'Microsoft', N'link')
INSERT [dbo].[Company] ([id], [name], [img]) VALUES (3, N'FPT Software', N'link')
GO
SET IDENTITY_INSERT [dbo].[Course] ON 

INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (1, N'Introduction to Python Programming', 1, CAST(49.99 AS Decimal(10, 2)), N'Learn Python programming basics and fundamentals.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 2, 70, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (2, N'UI/UX Design Principles', 2, CAST(79.99 AS Decimal(10, 2)), N'Explore principles of user interface and user experience design.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 3, 80, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (3, N'Digital Marketing Strategies', 3, CAST(59.99 AS Decimal(10, 2)), N'Discover effective digital marketing strategies and techniques.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 4, 75, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (4, N'Healthy Lifestyle Habits', 4, CAST(29.99 AS Decimal(10, 2)), N'Learn practical tips and habits for a healthy lifestyle.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 6, 60, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (5, N'Photography Masterclass', 4, CAST(89.99 AS Decimal(10, 2)), N'Master the art of photography with professional techniques.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 5, 85, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (6, N'Video Production Essentials', 5, CAST(69.99 AS Decimal(10, 2)), N'Essential skills and tools for producing high-quality videos.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 2, 80, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (7, N'Advanced Data Structures in C++', 6, CAST(99.99 AS Decimal(10, 2)), N'Advanced data structures and algorithms in C++ programming language.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 3, 85, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (8, N'Introduction to Web Development', 2, CAST(49.99 AS Decimal(10, 2)), N'Start your journey into web development with HTML, CSS, and JavaScript.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 5, 70, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (9, N'Effective Communication Skills', 3, CAST(39.99 AS Decimal(10, 2)), N'Develop effective communication skills for personal and professional success.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 6, 65, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (10, N'Financial Planning and Budgeting', 1, CAST(79.99 AS Decimal(10, 2)), N'Learn how to plan your finances and create effective budgets.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 5, 75, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (11, N'Data Science with R', 1, CAST(59.99 AS Decimal(10, 2)), N'An introductory course on data science using R programming language.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 2, 75, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (12, N'Graphic Design Basics', 2, CAST(49.99 AS Decimal(10, 2)), N'Learn the basics of graphic design and essential tools.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 3, 70, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (13, N'Social Media Marketing', 3, CAST(39.99 AS Decimal(10, 2)), N'Effective strategies for marketing on social media platforms.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 4, 65, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (14, N'Personal Development and Wellness', 4, CAST(29.99 AS Decimal(10, 2)), N'Techniques for improving personal development and wellness.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 5, 60, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (15, N'Advanced Photography Techniques', 5, CAST(89.99 AS Decimal(10, 2)), N'Advanced techniques for professional photography.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 6, 85, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (16, N'Video Editing for Beginners', 6, CAST(69.99 AS Decimal(10, 2)), N'A beginner?s guide to video editing and essential tools.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 2, 80, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (17, N'Machine Learning with Python', 1, CAST(99.99 AS Decimal(10, 2)), N'Advanced machine learning concepts and applications using Python.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 3, 85, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (18, N'User Experience Research', 2, CAST(79.99 AS Decimal(10, 2)), N'Methods and tools for conducting user experience research.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 4, 80, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (19, N'Content Marketing Strategies', 3, CAST(59.99 AS Decimal(10, 2)), N'Effective strategies for content marketing.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 5, 75, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (20, N'Mindfulness and Meditation', 4, CAST(29.99 AS Decimal(10, 2)), N'Learn techniques for mindfulness and meditation.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 6, 60, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (21, N'Portrait Photography', 5, CAST(89.99 AS Decimal(10, 2)), N'Master the art of portrait photography.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 2, 85, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (22, N'Advanced Videography', 6, CAST(99.99 AS Decimal(10, 2)), N'Advanced techniques and tools for professional videography.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 3, 90, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (23, N'Data Analysis with Excel', 1, CAST(49.99 AS Decimal(10, 2)), N'Learn how to analyze data effectively using Excel.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 4, 70, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (24, N'Design Thinking', 2, CAST(79.99 AS Decimal(10, 2)), N'An introduction to design thinking principles and practices.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 5, 80, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (25, N'SEO Best Practices', 3, CAST(59.99 AS Decimal(10, 2)), N'Learn the best practices for search engine optimization.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 6, 75, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (26, N'Healthy Eating Habits', 4, CAST(29.99 AS Decimal(10, 2)), N'Develop healthy eating habits for a better lifestyle.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 2, 65, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (27, N'Landscape Photography', 5, CAST(89.99 AS Decimal(10, 2)), N'Techniques for capturing stunning landscape photos.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 3, 85, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (28, N'Film Production Basics', 6, CAST(69.99 AS Decimal(10, 2)), N'Learn the basics of film production and essential tools.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 4, 80, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (29, N'Introduction to SQL', 1, CAST(49.99 AS Decimal(10, 2)), N'Learn SQL for database management and data analysis.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 5, 70, NULL)
INSERT [dbo].[Course] ([id], [name], [category_id], [price], [description], [created_at], [mentor_id], [pass_condition], [thumbnail_id]) VALUES (30, N'Web Accessibility', 2, CAST(79.99 AS Decimal(10, 2)), N'Best practices for creating accessible web designs.', CAST(N'2024-07-11T22:37:28.167' AS DateTime), 6, 80, NULL)
SET IDENTITY_INSERT [dbo].[Course] OFF
GO
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (1, 1)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (1, 2)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (2, 2)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (2, 3)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (3, 3)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (3, 4)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (4, 4)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (4, 5)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (5, 5)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (5, 6)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (6, 1)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (6, 6)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (7, 3)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (7, 7)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (8, 2)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (8, 7)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (9, 4)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (9, 8)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (10, 5)
INSERT [dbo].[CourseLearningPath] ([learning_path_id], [course_id]) VALUES (10, 8)
GO
INSERT [dbo].[CredentialIssued] ([id], [sourcetemplate_id], [user_id], [credentialcode], [certified_at]) VALUES (1, 2, 3, N'123241', CAST(N'2024-06-24T12:00:00.000' AS DateTime))
INSERT [dbo].[CredentialIssued] ([id], [sourcetemplate_id], [user_id], [credentialcode], [certified_at]) VALUES (2, 3, 3, N'453232', CAST(N'2024-06-24T12:00:00.000' AS DateTime))
INSERT [dbo].[CredentialIssued] ([id], [sourcetemplate_id], [user_id], [credentialcode], [certified_at]) VALUES (3, 9, 1, N'214234', CAST(N'2024-06-24T12:00:00.000' AS DateTime))
INSERT [dbo].[CredentialIssued] ([id], [sourcetemplate_id], [user_id], [credentialcode], [certified_at]) VALUES (4, 10, 4, N'132411', CAST(N'2024-06-24T12:00:00.000' AS DateTime))
INSERT [dbo].[CredentialIssued] ([id], [sourcetemplate_id], [user_id], [credentialcode], [certified_at]) VALUES (5, 4, 1, N'234355', CAST(N'2024-06-24T12:00:00.000' AS DateTime))
INSERT [dbo].[CredentialIssued] ([id], [sourcetemplate_id], [user_id], [credentialcode], [certified_at]) VALUES (6, 11, 1, N'143452', CAST(N'2024-06-24T12:00:00.000' AS DateTime))
GO
SET IDENTITY_INSERT [dbo].[DirectMessage] ON 

INSERT [dbo].[DirectMessage] ([id], [user1], [user2], [created_at]) VALUES (1, 1, 2, CAST(N'2024-07-18T06:05:13.833' AS DateTime))
INSERT [dbo].[DirectMessage] ([id], [user1], [user2], [created_at]) VALUES (2, 1, 3, CAST(N'2024-07-18T06:05:13.833' AS DateTime))
INSERT [dbo].[DirectMessage] ([id], [user1], [user2], [created_at]) VALUES (3, 2, 3, CAST(N'2024-07-18T06:05:13.833' AS DateTime))
INSERT [dbo].[DirectMessage] ([id], [user1], [user2], [created_at]) VALUES (4, 2, 4, CAST(N'2024-07-18T06:05:13.833' AS DateTime))
SET IDENTITY_INSERT [dbo].[DirectMessage] OFF
GO
SET IDENTITY_INSERT [dbo].[Discussion] ON 

INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (1, 2, 1, NULL, N'I found the introduction to Python programming quite engaging. Looking forward to diving deeper into variables and control structures!', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (2, 3, 2, NULL, N'The UI/UX design principles course is really insightful. Anyone else excited about learning prototyping techniques?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (3, 4, 3, NULL, N'Digital marketing strategies are evolving rapidly. Let''s discuss effective SEO tactics and social media engagement strategies.', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (4, 5, 4, NULL, N'Healthy lifestyle habits have made a big difference in my daily routine. What are your favorite tips for staying healthy?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (5, 6, 5, NULL, N'Photography masterclass has helped me capture some amazing shots. What are your thoughts on advanced techniques like lighting and composition?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (6, 7, 6, NULL, N'Video production essentials course is great for beginners. Who else is learning the basics of video editing and production?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (7, 8, 4, NULL, N'I''m curious about advanced data structures in C++. Any tips on mastering complex algorithms?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (8, 9, 2, NULL, N'UI/UX design is more than just aesthetics. How do you approach creating intuitive user interfaces?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (9, 10, 3, NULL, N'Effective communication skills are crucial in every aspect of life. Share your experiences and tips for improving communication.', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (10, 11, 5, NULL, N'Advanced photography techniques are challenging but rewarding. What techniques have you found most useful?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (11, 12, 6, NULL, N'Video editing for beginners has been a fun journey so far. What software do you recommend for beginners?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (12, 13, 1, NULL, N'Python programming language is versatile. What projects are you working on to apply your Python skills?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (13, 14, 3, NULL, N'Content marketing strategies are essential for digital success. Let''s discuss innovative content ideas and strategies.', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (14, 15, 4, NULL, N'Personal development and wellness tips have really helped me stay focused. How do you maintain a healthy work-life balance?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
INSERT [dbo].[Discussion] ([id], [user_id], [lesson_id], [parent_discussion_id], [content], [created_at]) VALUES (15, 16, 2, NULL, N'Learning about web accessibility has opened my eyes to creating inclusive designs. What are your thoughts on accessible web development?', CAST(N'2024-07-11T22:37:28.200' AS DateTime))
SET IDENTITY_INSERT [dbo].[Discussion] OFF
GO
INSERT [dbo].[Education] ([id], [degree], [university_id], [user_id]) VALUES (1, N'Bachelor degree', 1, 1)
INSERT [dbo].[Education] ([id], [degree], [university_id], [user_id]) VALUES (2, N'Master degree', 2, 2)
INSERT [dbo].[Education] ([id], [degree], [university_id], [user_id]) VALUES (3, N'Master of Science', 3, 3)
GO
SET IDENTITY_INSERT [dbo].[Emoji] ON 

INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (1, N'U+1F600', N'Grinning Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (2, N'U+1F603', N'Grinning Face with Big Eyes')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (3, N'U+1F604', N'Grinning Face with Smiling Eyes')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (4, N'U+1F601', N'Beaming Face with Smiling Eyes')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (5, N'U+1F606', N'Grinning Squinting Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (6, N'U+1F605', N'Grinning Face with Sweat')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (7, N'U+1F923', N'Rolling on the Floor Laughing')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (8, N'U+1F602', N'Face with Tears of Joy')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (9, N'U+1F642', N'Slightly Smiling Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (10, N'U+1F643', N'Upside-Down Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (11, N'U+1F609', N'Winking Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (12, N'U+1F60A', N'Smiling Face with Smiling Eyes')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (13, N'U+1F607', N'Smiling Face with Halo')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (14, N'U+1F970', N'Smiling Face with Hearts')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (15, N'U+1F60D', N'Smiling Face with Heart-Eyes')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (16, N'U+1F929', N'Star-Struck')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (17, N'U+1F618', N'Face Blowing a Kiss')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (18, N'U+1F617', N'Kissing Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (19, N'U+263A', N'Smiling Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (20, N'U+1F61A', N'Kissing Face with Closed Eyes')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (21, N'U+1F619', N'Kissing Face with Smiling Eyes')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (22, N'U+1F60B', N'Face Savoring Food')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (23, N'U+1F61B', N'Face with Tongue')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (24, N'U+1F61C', N'Winking Face with Tongue')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (25, N'U+1F92A', N'Zany Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (26, N'U+1F61D', N'Squinting Face with Tongue')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (27, N'U+1F911', N'Money-Mouth Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (28, N'U+1F917', N'Hugging Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (29, N'U+1F92D', N'Face with Hand Over Mouth')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (30, N'U+1F92B', N'Shushing Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (31, N'U+1F914', N'Thinking Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (32, N'U+1F910', N'Zipper-Mouth Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (33, N'U+1F928', N'Face with Raised Eyebrow')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (34, N'U+1F610', N'Neutral Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (35, N'U+1F611', N'Expressionless Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (36, N'U+1F636', N'Face Without Mouth')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (37, N'U+1F60F', N'Smirking Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (38, N'U+1F612', N'Unamused Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (39, N'U+1F644', N'Face with Rolling Eyes')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (40, N'U+1F62C', N'Grimacing Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (41, N'U+1F925', N'Lying Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (42, N'U+1F60C', N'Relieved Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (43, N'U+1F614', N'Pensive Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (44, N'U+1F62A', N'Sleepy Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (45, N'U+1F924', N'Drooling Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (46, N'U+1F634', N'Sleeping Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (47, N'U+1F637', N'Face with Medical Mask')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (48, N'U+1F912', N'Face with Thermometer')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (49, N'U+1F915', N'Face with Head-Bandage')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (50, N'U+1F922', N'Nauseated Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (51, N'U+1F92E', N'Face Vomiting')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (52, N'U+1F927', N'Sneezing Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (53, N'U+1F975', N'Hot Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (54, N'U+1F976', N'Cold Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (55, N'U+1F974', N'Woozy Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (56, N'U+1F635', N'Dizzy Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (57, N'U+1F92F', N'Exploding Head')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (58, N'U+9757', N'Cowboy Hat Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (59, N'U+1F920', N'Partying Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (60, N'U+1F973', N'Disguised Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (61, N'U+1F60E', N'Smiling Face with Sunglasses')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (62, N'U+1F913', N'Nerd Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (63, N'U+1F9D0', N'Face with Monocle')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (64, N'U+1F615', N'Confused Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (65, N'U+1F61F', N'Worried Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (66, N'U+1F641', N'Slightly Frowning Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (67, N'U+2639', N'Frowning Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (68, N'U+1F62E', N'Face with Open Mouth')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (69, N'U+1F62F', N'Hushed Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (70, N'U+1F632', N'Astonished Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (71, N'U+1F633', N'Flushed Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (72, N'U+1F97A', N'Pleading Face')
INSERT [dbo].[Emoji] ([id], [unicode], [name]) VALUES (73, N'U+1F626', N'Frowning Face with Open Mouth')
SET IDENTITY_INSERT [dbo].[Emoji] OFF
GO
INSERT [dbo].[Event] ([id], [title], [user_id], [views], [create_at]) VALUES (1, N'Zero to Hero - UI/UX Designers', 1, 0, CAST(N'2024-06-29T12:00:00.000' AS DateTime))
INSERT [dbo].[Event] ([id], [title], [user_id], [views], [create_at]) VALUES (2, N'Professional AI - Workshop', 1, 0, CAST(N'2024-07-02T12:00:00.000' AS DateTime))
INSERT [dbo].[Event] ([id], [title], [user_id], [views], [create_at]) VALUES (3, N'Hero to zero - Web Developers', 2, 0, CAST(N'2024-07-03T12:00:00.000' AS DateTime))
GO
SET IDENTITY_INSERT [dbo].[EventLog] ON 

INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (1, 7, 1, 3, NULL, CAST(N'2024-03-02T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (2, 7, 1, 1, NULL, CAST(N'2024-03-03T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (3, 7, 3, 2, NULL, CAST(N'2024-04-04T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (4, 7, 2, 3, NULL, CAST(N'2024-05-05T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (5, 7, 2, 1, NULL, CAST(N'2024-06-06T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (6, 7, 4, 3, NULL, CAST(N'2024-07-07T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (7, 7, 5, 3, NULL, CAST(N'2024-08-08T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (8, 8, 3, 3, NULL, CAST(N'2024-09-09T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (9, 8, 1, 3, NULL, CAST(N'2024-03-05T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (10, 8, 2, 1, NULL, CAST(N'2024-03-06T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (11, 8, 3, 2, NULL, CAST(N'2024-04-07T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (12, 8, 4, 3, NULL, CAST(N'2024-05-08T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (13, 9, 2, 1, NULL, CAST(N'2024-06-09T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (14, 9, 4, 3, NULL, CAST(N'2024-07-10T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (15, 9, 5, 3, NULL, CAST(N'2024-08-11T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (16, 9, 3, 3, NULL, CAST(N'2024-09-12T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (17, 9, 1, 3, NULL, CAST(N'2024-03-11T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (18, 7, 2, 1, NULL, CAST(N'2024-03-12T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (19, 7, 3, 2, NULL, CAST(N'2024-04-13T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (20, 7, 4, 3, NULL, CAST(N'2024-05-14T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (21, 10, 1, 3, NULL, CAST(N'2024-03-02T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (22, 10, 1, 1, NULL, CAST(N'2024-03-03T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (23, 13, 3, 2, NULL, CAST(N'2024-04-04T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (24, 14, 2, 3, NULL, CAST(N'2024-05-05T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (25, 15, 2, 1, NULL, CAST(N'2024-06-06T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (26, 16, 4, 3, NULL, CAST(N'2024-07-07T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (27, 7, 5, 3, NULL, CAST(N'2024-08-08T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (28, 8, 3, 3, NULL, CAST(N'2024-09-09T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (29, 9, 1, 3, NULL, CAST(N'2024-03-05T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (30, 10, 2, 1, NULL, CAST(N'2024-03-06T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (31, 11, 3, 2, NULL, CAST(N'2024-04-07T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (32, 12, 4, 3, NULL, CAST(N'2024-05-08T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (33, 13, 2, 1, NULL, CAST(N'2024-06-09T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (34, 14, 4, 3, NULL, CAST(N'2024-07-10T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (35, 15, 5, 3, NULL, CAST(N'2024-08-11T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (36, 16, 3, 3, NULL, CAST(N'2024-09-12T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (37, 7, 1, 3, NULL, CAST(N'2024-03-11T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (38, 8, 2, 1, NULL, CAST(N'2024-03-12T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (39, 9, 3, 2, NULL, CAST(N'2024-04-13T00:00:00.000' AS DateTime))
INSERT [dbo].[EventLog] ([id], [user_id], [source_id], [source_type_id], [event_type_id], [event_time]) VALUES (40, 10, 4, 3, NULL, CAST(N'2024-05-14T00:00:00.000' AS DateTime))
SET IDENTITY_INSERT [dbo].[EventLog] OFF
GO
SET IDENTITY_INSERT [dbo].[EventParameter] ON 

INSERT [dbo].[EventParameter] ([id], [name], [data_type], [event_type_id]) VALUES (1, N'workspace_id', N'int', 2)
INSERT [dbo].[EventParameter] ([id], [name], [data_type], [event_type_id]) VALUES (2, N'duration', N'int', 2)
SET IDENTITY_INSERT [dbo].[EventParameter] OFF
GO
SET IDENTITY_INSERT [dbo].[EventType] ON 

INSERT [dbo].[EventType] ([id], [event_type_name]) VALUES (1, N'Page View')
INSERT [dbo].[EventType] ([id], [event_type_name]) VALUES (2, N'Add to Cart')
INSERT [dbo].[EventType] ([id], [event_type_name]) VALUES (3, N'Purchase')
INSERT [dbo].[EventType] ([id], [event_type_name]) VALUES (4, N'Ad Impression')
INSERT [dbo].[EventType] ([id], [event_type_name]) VALUES (5, N'Ad Click')
INSERT [dbo].[EventType] ([id], [event_type_name]) VALUES (6, N'View Category')
SET IDENTITY_INSERT [dbo].[EventType] OFF
GO
SET IDENTITY_INSERT [dbo].[EventTypeMess] ON 

INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (1, N'User Login')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (2, N'User Online')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (3, N'User Logout')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (4, N'User Register')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (5, N'User Update')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (6, N'User Delete')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (7, N'User Block')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (8, N'User Unblock')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (9, N'User Change Password')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (10, N'User Forgot Password')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (11, N'User Reset Password')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (12, N'User Change Email')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (13, N'User Change Role')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (14, N'User Change Workspace')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (15, N'User Change Language')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (16, N'User Change Preference')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (17, N'User Change Notification Setting')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (18, N'User Change Navigation Bar')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (19, N'User Change Dark Mode')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (20, N'User Change Full Name')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (21, N'User Change DOB')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (22, N'User Change Email')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (23, N'User Change Avatar')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (24, N'User Change Status')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (25, N'User Change Phone Number')
INSERT [dbo].[EventTypeMess] ([id], [name]) VALUES (26, N'User Change Address')
SET IDENTITY_INSERT [dbo].[EventTypeMess] OFF
GO
INSERT [dbo].[EventUser] ([id], [event_id], [user_id]) VALUES (1, 1, 1)
INSERT [dbo].[EventUser] ([id], [event_id], [user_id]) VALUES (2, 1, 2)
INSERT [dbo].[EventUser] ([id], [event_id], [user_id]) VALUES (3, 1, 3)
INSERT [dbo].[EventUser] ([id], [event_id], [user_id]) VALUES (4, 2, 4)
GO
INSERT [dbo].[Experience] ([id], [jobtitle_id], [company_id], [type_id], [user_id], [isworking]) VALUES (1, 1, 1, 1, 1, 1)
INSERT [dbo].[Experience] ([id], [jobtitle_id], [company_id], [type_id], [user_id], [isworking]) VALUES (2, 3, 2, 2, 2, 1)
GO
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (7, 1)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (7, 2)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (7, 3)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (8, 4)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (8, 2)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (9, 5)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (9, 6)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (12, 3)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (11, 2)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (11, 1)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (10, 6)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (14, 1)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (15, 1)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (12, 4)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (8, 3)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (13, 2)
INSERT [dbo].[FavouriteCategory] ([mentee_id], [category_id]) VALUES (13, 1)
GO
SET IDENTITY_INSERT [dbo].[Feedback] ON 

INSERT [dbo].[Feedback] ([id], [user_id], [subsystem_id], [sender_email], [group_id], [status_id], [content], [send_at], [updated_at]) VALUES (1, 1, 1, N'test@gmail.com', 1, 2, N'Content 1', CAST(N'2024-07-18T06:05:13.927' AS DateTime), NULL)
INSERT [dbo].[Feedback] ([id], [user_id], [subsystem_id], [sender_email], [group_id], [status_id], [content], [send_at], [updated_at]) VALUES (2, 1, 2, N'test@gmail.com', 2, 1, N'Content 2', CAST(N'2024-07-18T06:05:13.927' AS DateTime), NULL)
INSERT [dbo].[Feedback] ([id], [user_id], [subsystem_id], [sender_email], [group_id], [status_id], [content], [send_at], [updated_at]) VALUES (3, 1, 1, N'test@gmail.com', 3, 1, N'Content 3', CAST(N'2024-07-18T06:05:13.927' AS DateTime), NULL)
INSERT [dbo].[Feedback] ([id], [user_id], [subsystem_id], [sender_email], [group_id], [status_id], [content], [send_at], [updated_at]) VALUES (4, 1, 1, N'test@gmail.com', 1, 3, N'Content 4', CAST(N'2024-07-18T06:05:13.927' AS DateTime), NULL)
SET IDENTITY_INSERT [dbo].[Feedback] OFF
GO
INSERT [dbo].[FeedbackAssignee] ([feedback_id], [assignee_id], [assign_at], [content]) VALUES (1, 4, CAST(N'2024-07-18T06:05:13.933' AS DateTime), N'Content 1')
GO
INSERT [dbo].[FeedbackAttachment] ([feedback_id], [asset_id]) VALUES (1, 1)
INSERT [dbo].[FeedbackAttachment] ([feedback_id], [asset_id]) VALUES (1, 2)
INSERT [dbo].[FeedbackAttachment] ([feedback_id], [asset_id]) VALUES (2, 1)
INSERT [dbo].[FeedbackAttachment] ([feedback_id], [asset_id]) VALUES (2, 2)
GO
SET IDENTITY_INSERT [dbo].[FeedbackGroup] ON 

INSERT [dbo].[FeedbackGroup] ([id], [name]) VALUES (1, N'Bug')
INSERT [dbo].[FeedbackGroup] ([id], [name]) VALUES (2, N'Feature Request')
INSERT [dbo].[FeedbackGroup] ([id], [name]) VALUES (3, N'Improvement')
INSERT [dbo].[FeedbackGroup] ([id], [name]) VALUES (4, N'Others')
SET IDENTITY_INSERT [dbo].[FeedbackGroup] OFF
GO
SET IDENTITY_INSERT [dbo].[FeedbackResult] ON 

INSERT [dbo].[FeedbackResult] ([id], [feedback_id], [content], [send_at]) VALUES (1, 4, N'Content 1', CAST(N'2024-07-18T06:05:13.940' AS DateTime))
SET IDENTITY_INSERT [dbo].[FeedbackResult] OFF
GO
SET IDENTITY_INSERT [dbo].[FeedbackStatus] ON 

INSERT [dbo].[FeedbackStatus] ([id], [name]) VALUES (1, N'Open')
INSERT [dbo].[FeedbackStatus] ([id], [name]) VALUES (2, N'In Progress')
INSERT [dbo].[FeedbackStatus] ([id], [name]) VALUES (3, N'Closed')
SET IDENTITY_INSERT [dbo].[FeedbackStatus] OFF
GO
INSERT [dbo].[FollowUser] ([id], [follower_id], [followee_id], [datefollow]) VALUES (1, 1, 2, CAST(N'2022-06-01T10:00:00.000' AS DateTime))
INSERT [dbo].[FollowUser] ([id], [follower_id], [followee_id], [datefollow]) VALUES (2, 4, 1, CAST(N'2023-05-15T14:30:00.000' AS DateTime))
INSERT [dbo].[FollowUser] ([id], [follower_id], [followee_id], [datefollow]) VALUES (3, 2, 1, CAST(N'2024-07-11T22:37:28.240' AS DateTime))
INSERT [dbo].[FollowUser] ([id], [follower_id], [followee_id], [datefollow]) VALUES (4, 3, 2, CAST(N'2024-07-11T22:37:28.240' AS DateTime))
GO
INSERT [dbo].[Jobtitle] ([id], [name]) VALUES (1, N'UI/UX Designer')
INSERT [dbo].[Jobtitle] ([id], [name]) VALUES (2, N'Senior Software Engineer')
INSERT [dbo].[Jobtitle] ([id], [name]) VALUES (3, N'CEO')
INSERT [dbo].[Jobtitle] ([id], [name]) VALUES (4, N'Mentor')
INSERT [dbo].[Jobtitle] ([id], [name]) VALUES (5, N'Data Scientist')
GO
SET IDENTITY_INSERT [dbo].[LearningPath] ON 

INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (1, N'Introduction to Information Technology', N'Learn the basics of Information Technology.', 2, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (2, N'UI/UX Design Fundamentals', N'Discover the principles of User Interface and User Experience design.', 2, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (3, N'Digital Marketing Essentials', N'Understand core concepts and strategies in digital marketing.', 3, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (4, N'Healthy Lifestyle Journey', N'Explore ways to lead a healthier lifestyle.', 4, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (5, N'Photography Techniques Masterclass', N'Master the fundamentals of photography.', 5, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (6, N'Video Production Basics', N'Learn essential skills for video production.', 2, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (7, N'Advanced Marketing Strategies', N'Explore advanced marketing techniques.', 3, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (8, N'IT Security Fundamentals', N'Understand the basics of IT security.', 2, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (9, N'Creative UI/UX Approaches', N'Explore creative approaches in UI/UX design.', 4, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
INSERT [dbo].[LearningPath] ([id], [title], [description], [mentor_id], [created_at], [updated_at]) VALUES (10, N'Fitness and Nutrition for Life', N'Discover the importance of fitness and nutrition.', 5, CAST(N'2024-07-11T22:37:28.220' AS DateTime), CAST(N'2024-07-11T22:37:28.220' AS DateTime))
SET IDENTITY_INSERT [dbo].[LearningPath] OFF
GO
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (1, 11, 0.1)
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (2, 12, 0.2)
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (3, 13, 0.3)
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (4, 14, 0.4)
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (5, 15, 0.5)
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (6, 16, 0.6)
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (7, 7, 0.7)
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (8, 8, 0.8)
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (9, 9, 0.9)
INSERT [dbo].[LearningPathProgress] ([learning_path_id], [mentee_id], [progress]) VALUES (10, 10, 1)
GO
SET IDENTITY_INSERT [dbo].[Lesson] ON 

INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (1, 1, N'Welcome to the Course', N'In this lesson, you will be introduced to the course and its objectives.', N'Introduction to the course and its objectives.', 1)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (2, 1, N'Course Overview', N'This lesson provides an overview of what will be covered throughout the course.', N'Overview of the course content and structure.', 2)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (3, 2, N'Understanding Variables', N'Learn about variables, their types, and how to declare them in programming.', N'Introduction to variables in programming.', 3)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (4, 2, N'Control Structures', N'Explore control structures such as if-statements, loops, and switch statements.', N'Introduction to control structures in programming.', 4)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (5, 3, N'Database Design Principles', N'Learn about database design principles, normalization, and entity-relationship modeling.', N'Advanced concepts in database design.', 5)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (6, 3, N'Web Security Best Practices', N'Explore best practices for securing web applications and preventing common vulnerabilities.', N'Advanced techniques for web security.', 6)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (7, 4, N'What is UI/UX?', N'Introduction to the concepts of UI/UX design.', N'Understanding UI/UX design basics.', 7)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (8, 4, N'History of UI/UX', N'An overview of the history and evolution of UI/UX design.', N'History and evolution of UI/UX design.', 8)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (9, 5, N'Design Elements', N'Learn about the basic elements of design.', N'Introduction to design elements.', 9)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (10, 5, N'Color Theory', N'Understanding color theory and its application in design.', N'Basics of color theory in design.', 10)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (11, 6, N'Prototyping', N'Learn about the process of creating prototypes.', N'Advanced techniques in prototyping.', 11)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (12, 6, N'User Testing', N'Methods and importance of user testing in UI/UX design.', N'Advanced techniques in user testing.', 12)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (13, 7, N'Digital Marketing Fundamentals', N'Introduction to the basics of digital marketing.', N'Understanding digital marketing basics.', 13)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (14, 7, N'Marketing Channels', N'Overview of different digital marketing channels.', N'Introduction to digital marketing channels.', 14)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (15, 8, N'Content Marketing', N'Strategies for effective content marketing.', N'Introduction to content marketing strategies.', 15)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (16, 8, N'SEO Basics', N'Understanding the basics of search engine optimization.', N'Basics of SEO in digital marketing.', 16)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (17, 9, N'Advanced SEO Techniques', N'Learn advanced techniques for search engine optimization.', N'Advanced SEO strategies.', 17)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (18, 9, N'Social Media Advertising', N'Strategies for effective social media advertising.', N'Advanced techniques in social media advertising.', 18)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (19, 10, N'Healthy Lifestyle Overview', N'Introduction to the principles of a healthy lifestyle.', N'Understanding healthy lifestyle basics.', 19)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (20, 10, N'Benefits of a Healthy Lifestyle', N'Explore the benefits of maintaining a healthy lifestyle.', N'Benefits of a healthy lifestyle.', 20)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (21, 11, N'Nutrition Basics', N'Understanding the basics of nutrition and healthy eating.', N'Basics of nutrition in healthy living.', 21)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (22, 11, N'Meal Planning', N'Tips for planning balanced and nutritious meals.', N'Introduction to meal planning.', 22)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (23, 12, N'Exercise Fundamentals', N'Basics of exercise and fitness.', N'Understanding exercise basics.', 23)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (24, 12, N'Creating a Fitness Plan', N'Learn how to create an effective fitness plan.', N'Introduction to fitness planning.', 24)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (25, 13, N'Photography Basics', N'Introduction to the basics of photography.', N'Understanding photography basics.', 25)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (26, 13, N'Camera Types', N'Overview of different types of cameras and their uses.', N'Basics of camera types in photography.', 26)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (27, 14, N'Lighting Techniques', N'Learn about various lighting techniques in photography.', N'Introduction to lighting techniques.', 27)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (28, 14, N'Composition and Framing', N'Understanding composition and framing in photography.', N'Basics of composition and framing.', 28)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (29, 15, N'Advanced Lighting', N'Advanced techniques in lighting for photography.', N'Advanced lighting techniques.', 29)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (30, 15, N'Post-Processing', N'Techniques for post-processing and editing photos.', N'Advanced post-processing techniques.', 30)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (31, 16, N'Video Production Basics', N'Introduction to the basics of video production.', N'Understanding video production basics.', 31)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (32, 16, N'Types of Video Equipment', N'Overview of different types of video equipment and their uses.', N'Basics of video equipment.', 32)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (33, 17, N'Editing Software', N'Learn about various video editing software options.', N'Introduction to video editing software.', 33)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (34, 17, N'Basic Editing Techniques', N'Understanding basic video editing techniques.', N'Basics of video editing.', 34)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (35, 18, N'Advanced Shooting Techniques', N'Advanced techniques for shooting professional videos.', N'Advanced shooting techniques.', 35)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (36, 18, N'Advanced Editing', N'Techniques for advanced video editing.', N'Advanced video editing techniques.', 36)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (37, 19, N'Data Structure Fundamentals', N'Introduction to the basics of data structures.', N'Understanding data structure basics.', 37)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (38, 19, N'Types of Data Structures', N'Overview of different types of data structures.', N'Basics of data structure types.', 38)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (39, 20, N'Linked Lists', N'Learn about linked lists and their applications.', N'Introduction to linked lists.', 39)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (40, 20, N'Stacks and Queues', N'Understanding stacks and queues in data structures.', N'Basics of stacks and queues.', 40)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (41, 21, N'Trees and Graphs', N'Advanced concepts in trees and graphs.', N'Advanced techniques in trees and graphs.', 41)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (42, 21, N'Hashing', N'Understanding the concept of hashing in data structures.', N'Advanced hashing techniques.', 42)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (43, 22, N'Web Development Overview', N'Introduction to the basics of web development.', N'Understanding web development basics.', 43)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (44, 22, N'HTML Basics', N'Learn about the basics of HTML for web development.', N'Basics of HTML in web development.', 44)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (45, 23, N'CSS Fundamentals', N'Introduction to the basics of CSS for web development.', N'Understanding CSS basics.', 45)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (46, 23, N'Styling with CSS', N'Learn how to style web pages using CSS.', N'Basics of styling with CSS.', 46)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (47, 24, N'JavaScript Basics', N'Introduction to the basics of JavaScript.', N'Understanding JavaScript basics.', 47)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (48, 24, N'DOM Manipulation', N'Learn how to manipulate the DOM using JavaScript.', N'Basics of DOM manipulation.', 48)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (49, 25, N'Communication Skills Overview', N'Introduction to the basics of effective communication.', N'Understanding communication skills basics.', 49)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (50, 25, N'Types of Communication', N'Overview of different types of communication.', N'Basics of communication types.', 50)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (51, 26, N'Public Speaking', N'Learn the basics of public speaking and presentation skills.', N'Introduction to public speaking.', 51)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (52, 26, N'Interpersonal Communication', N'Understanding the basics of interpersonal communication.', N'Basics of interpersonal communication.', 52)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (53, 27, N'Body Language', N'Learn about the importance of body language in communication.', N'Introduction to body language.', 53)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (54, 27, N'Facial Expressions', N'Understanding the role of facial expressions in communication.', N'Basics of facial expressions.', 54)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (55, 28, N'Financial Planning Basics', N'Introduction to the basics of financial planning.', N'Understanding financial planning basics.', 55)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (56, 28, N'Budgeting', N'Learn how to create and manage a budget effectively.', N'Basics of budgeting.', 56)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (57, 29, N'Saving Strategies', N'Learn effective strategies for saving money.', N'Introduction to saving strategies.', 57)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (58, 29, N'Debt Management', N'Understanding how to manage and reduce debt.', N'Basics of debt management.', 58)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (59, 30, N'Investing', N'Advanced techniques for investing and growing wealth.', N'Advanced investing techniques.', 59)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (60, 30, N'Retirement Planning', N'Understanding how to plan for a secure retirement.', N'Advanced retirement planning techniques.', 60)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (61, 11, N'Introduction to Data Science', N'Basics of data science using R.', N'Understanding data science basics.', 61)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (62, 11, N'R Programming', N'Basics of R programming language.', N'Introduction to R programming.', 62)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (63, 12, N'Design Basics', N'Introduction to graphic design.', N'Understanding graphic design basics.', 63)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (64, 12, N'Design Tools', N'Overview of essential design tools.', N'Basics of design tools.', 64)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (65, 13, N'Marketing Basics', N'Introduction to social media marketing.', N'Understanding marketing basics.', 65)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (66, 13, N'Marketing Tools', N'Overview of social media marketing tools.', N'Basics of marketing tools.', 66)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (67, 14, N'Personal Development', N'Introduction to personal development.', N'Understanding personal development basics.', 67)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (68, 14, N'Wellness Techniques', N'Overview of wellness techniques.', N'Basics of wellness techniques.', 68)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (69, 15, N'Photography Techniques', N'Advanced techniques in photography.', N'Understanding advanced photography techniques.', 69)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (70, 15, N'Editing Techniques', N'Advanced techniques in photo editing.', N'Basics of editing techniques.', 70)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (71, 16, N'Editing Basics', N'Introduction to video editing.', N'Understanding editing basics.', 71)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (72, 16, N'Editing Tools', N'Overview of video editing tools.', N'Basics of editing tools.', 72)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (73, 17, N'Machine Learning Basics', N'Introduction to machine learning.', N'Understanding machine learning basics.', 73)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (74, 17, N'Python for Machine Learning', N'Basics of using Python for machine learning.', N'Basics of Python in machine learning.', 74)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (75, 18, N'UX Research', N'Introduction to user experience research.', N'Understanding UX research basics.', 75)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (76, 18, N'Research Methods', N'Overview of research methods in UX.', N'Basics of research methods.', 76)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (77, 19, N'Content Marketing', N'Introduction to content marketing.', N'Understanding content marketing basics.', 77)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (78, 19, N'Marketing Strategies', N'Overview of content marketing strategies.', N'Basics of marketing strategies.', 78)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (79, 20, N'Mindfulness Basics', N'Introduction to mindfulness.', N'Understanding mindfulness basics.', 79)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (80, 20, N'Meditation Techniques', N'Overview of meditation techniques.', N'Basics of meditation techniques.', 80)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (81, 21, N'Portrait Techniques', N'Introduction to portrait photography.', N'Understanding portrait photography basics.', 81)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (82, 21, N'Lighting for Portraits', N'Overview of lighting techniques for portraits.', N'Basics of lighting for portraits.', 82)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (83, 22, N'Videography Basics', N'Introduction to advanced videography.', N'Understanding advanced videography basics.', 83)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (84, 22, N'Videography Techniques', N'Overview of advanced videography techniques.', N'Basics of videography techniques.', 84)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (85, 23, N'Excel Basics', N'Introduction to data analysis with Excel.', N'Understanding Excel basics.', 85)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (86, 23, N'Advanced Excel Techniques', N'Overview of advanced Excel techniques for data analysis.', N'Basics of advanced Excel techniques.', 86)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (87, 24, N'Design Thinking Basics', N'Introduction to design thinking.', N'Understanding design thinking basics.', 87)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (88, 24, N'Design Thinking Methods', N'Overview of design thinking methods.', N'Basics of design thinking methods.', 88)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (89, 25, N'SEO Basics', N'Introduction to SEO.', N'Understanding SEO basics.', 89)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (90, 25, N'Advanced SEO', N'Overview of advanced SEO techniques.', N'Basics of advanced SEO techniques.', 90)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (91, 26, N'Healthy Eating Basics', N'Introduction to healthy eating habits.', N'Understanding healthy eating habits basics.', 91)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (92, 26, N'Nutrition for Health', N'Overview of nutrition for health.', N'Basics of nutrition for health.', 92)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (93, 27, N'Landscape Techniques', N'Introduction to landscape photography.', N'Understanding landscape photography basics.', 93)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (94, 27, N'Editing Landscapes', N'Overview of editing techniques for landscape photography.', N'Basics of editing landscapes.', 94)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (95, 28, N'Film Production Basics', N'Introduction to film production.', N'Understanding film production basics.', 95)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (96, 28, N'Production Tools', N'Overview of film production tools.', N'Basics of production tools.', 96)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (97, 29, N'SQL Basics', N'Introduction to SQL.', N'Understanding SQL basics.', 97)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (98, 29, N'Advanced SQL', N'Overview of advanced SQL techniques.', N'Basics of advanced SQL techniques.', 98)
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (99, 30, N'Accessibility Basics', N'Introduction to web accessibility.', N'Understanding web accessibility basics.', 99)
GO
INSERT [dbo].[Lesson] ([id], [section_id], [title], [transcript], [summary], [asset_id]) VALUES (100, 30, N'Advanced Accessibility', N'Overview of advanced web accessibility techniques.', N'Basics of advanced web accessibility.', 100)
SET IDENTITY_INSERT [dbo].[Lesson] OFF
GO
INSERT [dbo].[Location] ([id], [name]) VALUES (1, N'Ho Chi Minh')
INSERT [dbo].[Location] ([id], [name]) VALUES (2, N'New York')
INSERT [dbo].[Location] ([id], [name]) VALUES (3, N'Ha Noi')
INSERT [dbo].[Location] ([id], [name]) VALUES (4, N'Chicago')
GO
SET IDENTITY_INSERT [dbo].[Log] ON 

INSERT [dbo].[Log] ([id], [user_id], [event_type_id], [log_time]) VALUES (1, 1, 2, CAST(N'2024-07-18T06:05:13.880' AS DateTime))
INSERT [dbo].[Log] ([id], [user_id], [event_type_id], [log_time]) VALUES (2, 2, 2, CAST(N'2024-07-18T06:05:13.880' AS DateTime))
INSERT [dbo].[Log] ([id], [user_id], [event_type_id], [log_time]) VALUES (3, 3, 2, CAST(N'2024-07-18T06:05:13.880' AS DateTime))
INSERT [dbo].[Log] ([id], [user_id], [event_type_id], [log_time]) VALUES (4, 4, 2, CAST(N'2024-07-18T06:05:13.880' AS DateTime))
INSERT [dbo].[Log] ([id], [user_id], [event_type_id], [log_time]) VALUES (5, 5, 2, CAST(N'2024-07-18T06:05:13.880' AS DateTime))
SET IDENTITY_INSERT [dbo].[Log] OFF
GO
SET IDENTITY_INSERT [dbo].[LogDetail] ON 

INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (1, 1, 1, N'1')
INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (2, 2, 1, N'1')
INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (3, 3, 1, N'1')
INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (4, 4, 1, N'1')
INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (5, 5, 1, N'1')
INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (6, 1, 2, N'20')
INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (7, 2, 2, N'30')
INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (8, 3, 2, N'40')
INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (9, 4, 2, N'50')
INSERT [dbo].[LogDetail] ([id], [log_id], [event_parameter_id], [value]) VALUES (10, 5, 2, N'60')
SET IDENTITY_INSERT [dbo].[LogDetail] OFF
GO
SET IDENTITY_INSERT [dbo].[Meeting] ON 

INSERT [dbo].[Meeting] ([id], [owner_id], [name], [description], [start_at], [end_at], [created_at]) VALUES (1, 1, N'Meeting 1', N'Description 1', CAST(N'2024-07-18T06:05:13.830' AS DateTime), CAST(N'2024-07-18T06:05:13.830' AS DateTime), CAST(N'2024-07-18T06:05:13.830' AS DateTime))
INSERT [dbo].[Meeting] ([id], [owner_id], [name], [description], [start_at], [end_at], [created_at]) VALUES (2, 1, N'Meeting 2', N'Description 2', CAST(N'2024-07-18T06:05:13.830' AS DateTime), CAST(N'2024-07-18T06:05:13.830' AS DateTime), CAST(N'2024-07-18T06:05:13.830' AS DateTime))
INSERT [dbo].[Meeting] ([id], [owner_id], [name], [description], [start_at], [end_at], [created_at]) VALUES (3, 2, N'Meeting 3', N'Description 3', CAST(N'2024-07-18T06:05:13.830' AS DateTime), CAST(N'2024-07-18T06:05:13.830' AS DateTime), CAST(N'2024-07-18T06:05:13.830' AS DateTime))
INSERT [dbo].[Meeting] ([id], [owner_id], [name], [description], [start_at], [end_at], [created_at]) VALUES (4, 2, N'Meeting 4', N'Description 4', CAST(N'2024-07-18T06:05:13.830' AS DateTime), CAST(N'2024-07-18T06:05:13.830' AS DateTime), CAST(N'2024-07-18T06:05:13.830' AS DateTime))
SET IDENTITY_INSERT [dbo].[Meeting] OFF
GO
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (1, 1, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (1, 2, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (1, 3, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (2, 1, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (2, 2, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (2, 3, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (3, 1, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (3, 2, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (3, 3, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (4, 1, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (4, 2, 1, NULL, NULL)
INSERT [dbo].[MeetingParticipant] ([meeting_id], [user_id], [status_id], [joined_at], [left_at]) VALUES (4, 3, 1, NULL, NULL)
GO
SET IDENTITY_INSERT [dbo].[MeetingParticipantStatus] ON 

INSERT [dbo].[MeetingParticipantStatus] ([id], [name]) VALUES (1, N'Invited')
INSERT [dbo].[MeetingParticipantStatus] ([id], [name]) VALUES (2, N'Accepted')
INSERT [dbo].[MeetingParticipantStatus] ([id], [name]) VALUES (3, N'Joined')
INSERT [dbo].[MeetingParticipantStatus] ([id], [name]) VALUES (4, N'Left')
INSERT [dbo].[MeetingParticipantStatus] ([id], [name]) VALUES (5, N'Declined')
SET IDENTITY_INSERT [dbo].[MeetingParticipantStatus] OFF
GO
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (7, 1, 50, CAST(N'2024-05-26T18:32:01.000' AS DateTime), 1, CAST(N'2023-02-28' AS Date), CAST(N'2024-02-28' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (7, 2, 70, CAST(N'2024-05-27T18:32:01.000' AS DateTime), 2, CAST(N'2023-03-15' AS Date), CAST(N'2024-03-15' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (8, 3, 30, CAST(N'2024-05-28T18:32:01.000' AS DateTime), NULL, NULL, NULL)
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (8, 4, 80, CAST(N'2024-05-29T18:32:01.000' AS DateTime), 3, CAST(N'2023-03-30' AS Date), CAST(N'2024-03-30' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (9, 5, 60, CAST(N'2024-05-25T18:32:01.000' AS DateTime), 4, CAST(N'2023-03-01' AS Date), CAST(N'2024-03-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (9, 6, 90, CAST(N'2024-05-25T18:32:01.000' AS DateTime), 5, CAST(N'2023-04-10' AS Date), CAST(N'2024-04-10' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (10, 7, 40, CAST(N'2024-05-25T18:32:01.000' AS DateTime), NULL, NULL, NULL)
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (10, 8, 85, CAST(N'2024-05-25T18:32:01.000' AS DateTime), 6, CAST(N'2023-04-15' AS Date), CAST(N'2024-04-15' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (8, 1, 75, CAST(N'2024-04-25T18:32:01.000' AS DateTime), 7, CAST(N'2023-03-15' AS Date), CAST(N'2024-03-15' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (9, 2, 95, CAST(N'2024-04-25T18:32:01.000' AS DateTime), 8, CAST(N'2023-04-20' AS Date), CAST(N'2024-04-20' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (11, 3, 55, CAST(N'2024-04-25T18:32:01.000' AS DateTime), 9, CAST(N'2023-05-01' AS Date), CAST(N'2024-05-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (11, 4, 78, CAST(N'2024-04-25T18:32:01.000' AS DateTime), 10, CAST(N'2023-05-10' AS Date), CAST(N'2024-05-10' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (12, 5, 68, CAST(N'2024-04-25T18:32:01.000' AS DateTime), 11, CAST(N'2023-06-01' AS Date), CAST(N'2024-06-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (12, 6, 87, CAST(N'2024-04-25T18:32:01.000' AS DateTime), 12, CAST(N'2023-06-15' AS Date), CAST(N'2024-06-15' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (13, 7, 42, CAST(N'2024-05-25T18:32:01.000' AS DateTime), 13, CAST(N'2023-07-01' AS Date), CAST(N'2024-07-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (13, 8, 82, CAST(N'2024-05-25T18:32:01.000' AS DateTime), 14, CAST(N'2023-07-10' AS Date), CAST(N'2024-07-10' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (14, 1, 91, CAST(N'2024-05-25T18:32:01.000' AS DateTime), 15, CAST(N'2023-08-01' AS Date), CAST(N'2024-08-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (14, 2, 63, CAST(N'2024-05-25T18:32:01.000' AS DateTime), 16, CAST(N'2023-08-15' AS Date), CAST(N'2024-08-15' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (15, 3, 73, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 17, CAST(N'2023-09-01' AS Date), CAST(N'2024-09-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (15, 4, 84, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 18, CAST(N'2023-09-10' AS Date), CAST(N'2024-09-10' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (16, 5, 57, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 19, CAST(N'2023-10-01' AS Date), CAST(N'2024-10-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (16, 6, 89, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 20, CAST(N'2023-10-15' AS Date), CAST(N'2024-10-15' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (11, 7, 60, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 21, CAST(N'2023-11-01' AS Date), CAST(N'2024-11-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (11, 8, 82, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 22, CAST(N'2023-11-10' AS Date), CAST(N'2024-11-10' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (12, 1, 45, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 23, CAST(N'2023-12-01' AS Date), CAST(N'2024-12-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (12, 2, 78, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 24, CAST(N'2023-12-15' AS Date), CAST(N'2024-12-15' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (13, 3, 65, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 25, CAST(N'2024-01-01' AS Date), CAST(N'2025-01-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (13, 4, 88, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 26, CAST(N'2024-01-10' AS Date), CAST(N'2025-01-10' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (14, 5, 70, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 27, CAST(N'2024-02-01' AS Date), CAST(N'2025-02-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (14, 6, 92, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 28, CAST(N'2024-02-15' AS Date), CAST(N'2025-02-15' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (15, 7, 55, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 29, CAST(N'2024-03-01' AS Date), CAST(N'2025-03-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (15, 8, 83, CAST(N'2024-06-25T18:32:01.000' AS DateTime), 30, CAST(N'2024-03-10' AS Date), CAST(N'2025-03-10' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (16, 1, 75, CAST(N'2024-06-25T18:32:01.000' AS DateTime), NULL, NULL, NULL)
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (16, 2, 90, CAST(N'2024-06-25T18:32:01.000' AS DateTime), NULL, NULL, NULL)
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (7, 3, 60, CAST(N'2024-07-25T18:32:01.000' AS DateTime), 31, CAST(N'2024-04-01' AS Date), CAST(N'2025-04-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (7, 4, 80, CAST(N'2024-07-25T18:32:01.000' AS DateTime), 32, CAST(N'2024-04-10' AS Date), CAST(N'2025-04-10' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (8, 5, 70, CAST(N'2024-07-25T18:32:01.000' AS DateTime), 33, CAST(N'2024-05-01' AS Date), CAST(N'2025-05-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (8, 6, 95, CAST(N'2024-07-25T18:32:01.000' AS DateTime), 34, CAST(N'2024-05-15' AS Date), CAST(N'2025-05-15' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (9, 7, 50, CAST(N'2024-07-25T18:32:01.000' AS DateTime), 35, CAST(N'2024-06-01' AS Date), CAST(N'2025-06-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (9, 8, 85, CAST(N'2024-07-25T18:32:01.000' AS DateTime), 36, CAST(N'2024-06-10' AS Date), CAST(N'2025-06-10' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (10, 1, 65, CAST(N'2024-07-25T18:32:01.000' AS DateTime), 37, CAST(N'2024-07-01' AS Date), CAST(N'2025-07-01' AS Date))
INSERT [dbo].[MenteeCourse] ([mentee_id], [course_id], [progress], [enroll_at], [cert_id], [issued_on], [expiry_at]) VALUES (10, 2, 92, CAST(N'2024-07-25T18:32:01.000' AS DateTime), 38, CAST(N'2024-07-15' AS Date), CAST(N'2025-07-15' AS Date))
GO
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (11, 1, 4.5)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (11, 2, 9.5)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (11, 3, 5)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (11, 4, 10)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (12, 1, 3)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (12, 2, 7)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (12, 3, 4.5)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (12, 4, 8)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (13, 5, 4.5)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (13, 6, 9)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (13, 7, 5)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (13, 8, 10)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (14, 5, 3)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (14, 6, 7.5)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (14, 7, 4)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (14, 8, 8.5)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (15, 9, 4)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (15, 10, 8)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (15, 11, 5)
INSERT [dbo].[MenteeQuestion] ([mentee_id], [question_id], [earned_marks]) VALUES (15, 12, 10)
GO
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (1, 7)
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (2, 8)
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (3, 13)
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (4, 14)
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (5, 15)
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (6, 16)
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (7, 7)
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (8, 8)
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (9, 9)
INSERT [dbo].[MenteeSaveCourse] ([course_id], [mentee_id]) VALUES (10, 10)
GO
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (1, 1, 2, 5, N'Excellent work!')
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (2, 2, 3, 4, N'Very helpful and insightful.')
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (3, 3, 4, 3, N'Good mentee, but can improve.')
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (4, 4, 5, 5, N'Amazing job. Highly recommend!')
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (5, 5, 6, 2, N'Needs to be more punctual.')
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (6, 1, 3, 4, N'Provided great scored.')
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (7, 2, 4, 5, N'Exceptional mentee, very knowledgeable.')
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (8, 3, 5, 3, N'Very good, smart guys.')
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (9, 4, 6, 4, N'Great mentee, very supportive.')
INSERT [dbo].[MentorReview] ([id], [sender_id], [receiver_id], [rating_star], [content]) VALUES (10, 5, 1, 5, N'Outstanding guidance and support.')
GO
SET IDENTITY_INSERT [dbo].[Message] ON 

INSERT [dbo].[Message] ([id], [sender_id], [content], [channel_id], [dms_id], [parent_id], [meeting_id], [status_id], [send_at], [edited_at], [is_deleted], [deleted_at]) VALUES (1, 1, N'Message 1', 1, NULL, NULL, NULL, NULL, CAST(N'2024-07-18T06:05:13.900' AS DateTime), NULL, 0, NULL)
INSERT [dbo].[Message] ([id], [sender_id], [content], [channel_id], [dms_id], [parent_id], [meeting_id], [status_id], [send_at], [edited_at], [is_deleted], [deleted_at]) VALUES (2, 1, N'Message 2', 1, NULL, NULL, NULL, NULL, CAST(N'2024-07-18T06:05:13.900' AS DateTime), NULL, 0, NULL)
INSERT [dbo].[Message] ([id], [sender_id], [content], [channel_id], [dms_id], [parent_id], [meeting_id], [status_id], [send_at], [edited_at], [is_deleted], [deleted_at]) VALUES (3, 1, N'Message 3', 2, NULL, NULL, NULL, NULL, CAST(N'2024-07-18T06:05:13.900' AS DateTime), NULL, 0, NULL)
INSERT [dbo].[Message] ([id], [sender_id], [content], [channel_id], [dms_id], [parent_id], [meeting_id], [status_id], [send_at], [edited_at], [is_deleted], [deleted_at]) VALUES (4, 1, N'Message 4', 2, NULL, NULL, NULL, NULL, CAST(N'2024-07-18T06:05:13.900' AS DateTime), NULL, 0, NULL)
INSERT [dbo].[Message] ([id], [sender_id], [content], [channel_id], [dms_id], [parent_id], [meeting_id], [status_id], [send_at], [edited_at], [is_deleted], [deleted_at]) VALUES (5, 1, N'Message 1', NULL, 1, NULL, NULL, NULL, CAST(N'2024-07-18T06:05:13.903' AS DateTime), NULL, 0, NULL)
INSERT [dbo].[Message] ([id], [sender_id], [content], [channel_id], [dms_id], [parent_id], [meeting_id], [status_id], [send_at], [edited_at], [is_deleted], [deleted_at]) VALUES (6, 1, N'Message 2', NULL, 1, NULL, NULL, NULL, CAST(N'2024-07-18T06:05:13.903' AS DateTime), NULL, 0, NULL)
INSERT [dbo].[Message] ([id], [sender_id], [content], [channel_id], [dms_id], [parent_id], [meeting_id], [status_id], [send_at], [edited_at], [is_deleted], [deleted_at]) VALUES (7, 1, N'Message 3', NULL, 2, NULL, NULL, NULL, CAST(N'2024-07-18T06:05:13.903' AS DateTime), NULL, 0, NULL)
INSERT [dbo].[Message] ([id], [sender_id], [content], [channel_id], [dms_id], [parent_id], [meeting_id], [status_id], [send_at], [edited_at], [is_deleted], [deleted_at]) VALUES (8, 1, N'Message 4', NULL, 2, NULL, NULL, NULL, CAST(N'2024-07-18T06:05:13.903' AS DateTime), NULL, 0, NULL)
SET IDENTITY_INSERT [dbo].[Message] OFF
GO
INSERT [dbo].[MessageAttachment] ([message_id], [asset_id]) VALUES (1, 1)
INSERT [dbo].[MessageAttachment] ([message_id], [asset_id]) VALUES (1, 2)
INSERT [dbo].[MessageAttachment] ([message_id], [asset_id]) VALUES (2, 1)
INSERT [dbo].[MessageAttachment] ([message_id], [asset_id]) VALUES (2, 2)
GO
INSERT [dbo].[MessageMention] ([message_id], [user_id]) VALUES (1, 1)
INSERT [dbo].[MessageMention] ([message_id], [user_id]) VALUES (1, 2)
INSERT [dbo].[MessageMention] ([message_id], [user_id]) VALUES (2, 1)
INSERT [dbo].[MessageMention] ([message_id], [user_id]) VALUES (2, 2)
GO
INSERT [dbo].[MessageReaction] ([message_id], [emoji_id], [user_id]) VALUES (1, 1, 1)
INSERT [dbo].[MessageReaction] ([message_id], [emoji_id], [user_id]) VALUES (1, 2, 1)
INSERT [dbo].[MessageReaction] ([message_id], [emoji_id], [user_id]) VALUES (2, 1, 1)
INSERT [dbo].[MessageReaction] ([message_id], [emoji_id], [user_id]) VALUES (2, 2, 1)
GO
SET IDENTITY_INSERT [dbo].[NotificationQueue] ON 

INSERT [dbo].[NotificationQueue] ([id], [user_id], [notification_type_id], [content], [is_read]) VALUES (1, 1, 4, N'Content 1', 0)
INSERT [dbo].[NotificationQueue] ([id], [user_id], [notification_type_id], [content], [is_read]) VALUES (2, 1, 4, N'Content 2', 0)
INSERT [dbo].[NotificationQueue] ([id], [user_id], [notification_type_id], [content], [is_read]) VALUES (3, 1, 4, N'Content 3', 0)
INSERT [dbo].[NotificationQueue] ([id], [user_id], [notification_type_id], [content], [is_read]) VALUES (4, 1, 4, N'Content 4', 0)
INSERT [dbo].[NotificationQueue] ([id], [user_id], [notification_type_id], [content], [is_read]) VALUES (5, 1, 4, N'Content 5', 0)
INSERT [dbo].[NotificationQueue] ([id], [user_id], [notification_type_id], [content], [is_read]) VALUES (6, 1, 4, N'Content 6', 0)
SET IDENTITY_INSERT [dbo].[NotificationQueue] OFF
GO
SET IDENTITY_INSERT [dbo].[NotificationType] ON 

INSERT [dbo].[NotificationType] ([id], [name]) VALUES (1, N'Email')
INSERT [dbo].[NotificationType] ([id], [name]) VALUES (2, N'SMS')
INSERT [dbo].[NotificationType] ([id], [name]) VALUES (3, N'Push Notification')
INSERT [dbo].[NotificationType] ([id], [name]) VALUES (4, N'In-App Message')
SET IDENTITY_INSERT [dbo].[NotificationType] OFF
GO
SET IDENTITY_INSERT [dbo].[Order] ON 

INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (1, 11, 1, 1, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (2, 12, 2, 2, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (3, 13, 3, 1, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (4, 14, 4, 2, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (5, 15, 5, 1, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (6, 16, 6, 2, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (7, 7, 7, 1, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (8, 8, 8, 2, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (9, 9, 9, 1, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
INSERT [dbo].[Order] ([id], [user_id], [user_payment_id], [status], [created_at]) VALUES (10, 10, 10, 2, CAST(N'2024-07-11T22:37:28.210' AS DateTime))
SET IDENTITY_INSERT [dbo].[Order] OFF
GO
SET IDENTITY_INSERT [dbo].[OrderDetail] ON 

INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (1, 1, CAST(49.99 AS Decimal(10, 2)), 1, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (2, 1, CAST(29.99 AS Decimal(10, 2)), 2, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (3, 1, CAST(19.99 AS Decimal(10, 2)), 3, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (4, 2, CAST(79.99 AS Decimal(10, 2)), 4, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (5, 2, CAST(59.99 AS Decimal(10, 2)), 5, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (6, 3, CAST(29.99 AS Decimal(10, 2)), 6, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (7, 4, CAST(89.99 AS Decimal(10, 2)), 7, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (8, 4, CAST(99.99 AS Decimal(10, 2)), 8, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (9, 5, CAST(69.99 AS Decimal(10, 2)), 9, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (10, 5, CAST(39.99 AS Decimal(10, 2)), 10, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (11, 6, CAST(49.99 AS Decimal(10, 2)), 11, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (12, 6, CAST(79.99 AS Decimal(10, 2)), 12, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (13, 7, CAST(59.99 AS Decimal(10, 2)), 13, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (14, 7, CAST(29.99 AS Decimal(10, 2)), 14, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (15, 8, CAST(89.99 AS Decimal(10, 2)), 15, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (16, 8, CAST(69.99 AS Decimal(10, 2)), 16, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (17, 9, CAST(99.99 AS Decimal(10, 2)), 17, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (18, 9, CAST(49.99 AS Decimal(10, 2)), 18, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (19, 10, CAST(79.99 AS Decimal(10, 2)), 19, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (20, 10, CAST(39.99 AS Decimal(10, 2)), 20, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (21, 1, CAST(29.99 AS Decimal(10, 2)), 21, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (22, 1, CAST(89.99 AS Decimal(10, 2)), 22, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (23, 2, CAST(49.99 AS Decimal(10, 2)), 23, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (24, 2, CAST(69.99 AS Decimal(10, 2)), 24, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (25, 3, CAST(99.99 AS Decimal(10, 2)), 25, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (26, 3, CAST(59.99 AS Decimal(10, 2)), 26, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (27, 4, CAST(39.99 AS Decimal(10, 2)), 27, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (28, 4, CAST(29.99 AS Decimal(10, 2)), 28, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (29, 5, CAST(89.99 AS Decimal(10, 2)), 29, 1)
INSERT [dbo].[OrderDetail] ([id], [order_id], [price], [source_id], [source_type_id]) VALUES (30, 5, CAST(79.99 AS Decimal(10, 2)), 30, 1)
SET IDENTITY_INSERT [dbo].[OrderDetail] OFF
GO
SET IDENTITY_INSERT [dbo].[PaymentMethod] ON 

INSERT [dbo].[PaymentMethod] ([id], [method]) VALUES (1, N'Credit Card')
INSERT [dbo].[PaymentMethod] ([id], [method]) VALUES (2, N'Debit Card')
INSERT [dbo].[PaymentMethod] ([id], [method]) VALUES (3, N'PayPal')
INSERT [dbo].[PaymentMethod] ([id], [method]) VALUES (4, N'Bank Transfer')
INSERT [dbo].[PaymentMethod] ([id], [method]) VALUES (5, N'Cryptocurrency')
SET IDENTITY_INSERT [dbo].[PaymentMethod] OFF
GO
SET IDENTITY_INSERT [dbo].[PollAnswer] ON 

INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (1, 1, N'Answer 1', 1, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (2, 1, N'Answer 2', 1, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (3, 1, N'Answer 3', 1, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (4, 2, N'Answer 1', 2, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (5, 2, N'Answer 2', 2, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (6, 2, N'Answer 3', 2, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (7, 3, N'Answer 1', 1, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (8, 3, N'Answer 2', 1, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (9, 3, N'Answer 3', 1, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (10, 4, N'Answer 1', 2, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (11, 4, N'Answer 2', 2, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
INSERT [dbo].[PollAnswer] ([id], [question_id], [answer], [created_by], [created_at]) VALUES (12, 4, N'Answer 3', 2, CAST(N'2024-07-18T06:05:13.870' AS DateTime))
SET IDENTITY_INSERT [dbo].[PollAnswer] OFF
GO
SET IDENTITY_INSERT [dbo].[PollQuestion] ON 

INSERT [dbo].[PollQuestion] ([id], [question], [channel_id], [created_by], [created_at], [expires_at]) VALUES (1, N'Question 1', 1, 1, CAST(N'2024-07-18T06:05:13.863' AS DateTime), CAST(N'2024-07-18T06:05:13.863' AS DateTime))
INSERT [dbo].[PollQuestion] ([id], [question], [channel_id], [created_by], [created_at], [expires_at]) VALUES (2, N'Question 2', 1, 2, CAST(N'2024-07-18T06:05:13.863' AS DateTime), CAST(N'2024-07-18T06:05:13.863' AS DateTime))
INSERT [dbo].[PollQuestion] ([id], [question], [channel_id], [created_by], [created_at], [expires_at]) VALUES (3, N'Question 3', 2, 1, CAST(N'2024-07-18T06:05:13.863' AS DateTime), CAST(N'2024-07-18T06:05:13.863' AS DateTime))
INSERT [dbo].[PollQuestion] ([id], [question], [channel_id], [created_by], [created_at], [expires_at]) VALUES (4, N'Question 4', 2, 2, CAST(N'2024-07-18T06:05:13.863' AS DateTime), CAST(N'2024-07-18T06:05:13.863' AS DateTime))
SET IDENTITY_INSERT [dbo].[PollQuestion] OFF
GO
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (1, 1, 1, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (1, 2, 1, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (1, 3, 1, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (2, 1, 2, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (2, 2, 2, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (2, 3, 2, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (3, 1, 1, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (3, 2, 1, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (3, 3, 1, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (4, 1, 2, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (4, 2, 2, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
INSERT [dbo].[PollVotingHistory] ([question_id], [answer_id], [voted_by], [voted_at]) VALUES (4, 3, 2, CAST(N'2024-07-18T06:05:13.873' AS DateTime))
GO
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (1, 5, N'Software Engineering Fundamentals', N'Essential software engineering concepts', 33.99, 1, 101)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (2, 6, N'Data Science', N'Data analysis and machine learning mastery', 12.99, 1, 102)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (3, 5, N'Web Development Mastery', N'Interactive e-learning platform', 17.77, 1, 103)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (4, 6, N'Mentoring Hub', N'Personalized professional growth through mentorship', 19.99, 3, 104)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (5, 5, N'Digital Marketing Bootcamp', N'Comprehensive training in digital marketing strategies and tools', 99.99, 2, 105)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (6, 1, N'Machine Learning A-Z', N'Complete machine learning guide', 45.99, 1, 106)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (7, 2, N'Cloud Computing Basics', N'Introduction to cloud services and architecture', 29.99, 4, 107)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (8, 2, N'Cybersecurity Essentials', N'Fundamentals of cybersecurity practices', 39.99, 3, 108)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (9, 3, N'Advanced Java Programming', N'Deep dive into Java programming language', 55, 1, 109)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (10, 4, N'Blockchain and Cryptocurrency', N'Understanding blockchain technology and cryptocurrencies', 60, 4, 110)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (11, 5, N'Artificial Intelligence for Beginners', N'Basics of AI and its applications', 70, 1, 111)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (12, 3, N'Project Management Professional (PMP)', N'Comprehensive PMP certification prep', 80, 5, 112)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (13, 4, N'User Experience (UX) Design', N'Designing user-friendly interfaces', 50, 2, 113)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (14, 5, N'Mobile App Development with Flutter', N'Building mobile apps using Flutter', 65, 4, 114)
INSERT [dbo].[Program] ([id], [user_id], [program_name], [description], [price], [category_id], [asset_id]) VALUES (15, 1, N'DevOps and Continuous Integration', N'Introduction to DevOps practices and tools', 75, 1, 115)
GO
INSERT [dbo].[ProgramMentor] ([program_id], [user_id]) VALUES (1, 1)
INSERT [dbo].[ProgramMentor] ([program_id], [user_id]) VALUES (1, 2)
INSERT [dbo].[ProgramMentor] ([program_id], [user_id]) VALUES (2, 3)
INSERT [dbo].[ProgramMentor] ([program_id], [user_id]) VALUES (2, 6)
INSERT [dbo].[ProgramMentor] ([program_id], [user_id]) VALUES (3, 4)
INSERT [dbo].[ProgramMentor] ([program_id], [user_id]) VALUES (3, 5)
GO
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (2, 1, 1, 1)
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (2, 1, 2, 2)
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (2, 2, 1, 3)
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (2, 2, 2, 4)
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (3, 3, 1, 3)
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (3, 3, 2, 8)
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (4, 4, 1, 4)
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (4, 4, 2, 9)
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (5, 5, 1, 5)
INSERT [dbo].[ProgramSource] ([program_id], [source_id], [source_type_id], [source_order]) VALUES (5, 5, 2, 10)
GO
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (1, 1, 50, N'In Progress', CAST(N'2024-01-01' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (1, 2, 60, N'In Progress', CAST(N'2024-07-10' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (1, 3, 80, N'Completed', CAST(N'2024-07-25' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (1, 5, 70, N'In Progress', CAST(N'2024-07-05' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (2, 1, 69, N'In Progress', CAST(N'2024-04-01' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (2, 2, 30, N'In Progress', CAST(N'2024-02-01' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (2, 3, 45, N'In Progress', CAST(N'2024-06-15' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (2, 4, 90, N'Completed', CAST(N'2024-07-30' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (3, 1, 50, N'In Progress', CAST(N'2024-07-12' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (3, 3, 80, N'Completed', CAST(N'2024-03-01' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (3, 4, 90, N'Completed', CAST(N'2024-07-20' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (4, 1, 60, N'In Progress', CAST(N'2024-07-08' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (4, 2, 61, N'In Progress', CAST(N'2024-05-01' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (4, 3, 99, N'Completed', CAST(N'2024-06-01' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (5, 1, 70, N'In Progress', CAST(N'2024-07-15' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (5, 2, 95, N'Completed', CAST(N'2024-06-23' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (5, 4, 81, N'Completed', CAST(N'2024-07-01' AS Date))
INSERT [dbo].[ProgramUser] ([program_id], [user_id], [progress_percent], [status], [start_at]) VALUES (5, 6, 72, N'In Progress', CAST(N'2024-08-01' AS Date))
GO
SET IDENTITY_INSERT [dbo].[Question] ON 

INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (1, 1, 1, N'What is Information Technology?', 1, 5, N'Basic definition of Information Technology.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (2, 2, 1, N'List three examples of IT devices.', 0, 10, N'Examples include computers, smartphones, and servers.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (3, 1, 2, N'What does UI stand for?', 1, 5, N'UI stands for User Interface.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (4, 2, 2, N'Describe the main difference between UI and UX.', 0, 10, N'UI is about the look and feel, UX is about user experience.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (5, 1, 3, N'Define marketing.', 1, 5, N'Marketing is the process of promoting products or services.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (6, 2, 3, N'Explain the 4 Ps of marketing.', 0, 10, N'Product, Price, Place, Promotion.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (7, 1, 4, N'Why is a healthy lifestyle important?', 1, 5, N'A healthy lifestyle helps maintain physical and mental health.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (8, 2, 4, N'Give two benefits of regular exercise.', 0, 10, N'Benefits include improved fitness and mood.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (9, 1, 5, N'What is aperture in photography?', 1, 5, N'Aperture controls the amount of light entering the camera.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (10, 2, 5, N'Explain the rule of thirds in photography.', 0, 10, N'It is a composition technique for balancing images.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (11, 1, 6, N'What is video editing?', 1, 5, N'Video editing involves rearranging video shots to create a new work.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (12, 2, 6, N'List two popular video editing software.', 0, 10, N'Examples are Adobe Premiere Pro and Final Cut Pro.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (13, 1, 7, N'Define cloud computing.', 1, 5, N'Cloud computing is delivering computing services over the internet.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (14, 2, 7, N'Give one advantage and one disadvantage of cloud computing.', 0, 10, N'Advantage: scalability, Disadvantage: security risks.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (15, 1, 8, N'What is a wireframe in UI design?', 1, 5, N'A wireframe is a basic visual guide to suggest the structure of an interface.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (16, 2, 8, N'Explain the concept of user personas.', 0, 10, N'User personas are fictional characters created to represent different user types.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (17, 1, 9, N'What is a marketing funnel?', 1, 5, N'A marketing funnel is a model describing the customer journey.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (18, 2, 9, N'Describe the stages of a marketing funnel.', 0, 10, N'Stages include awareness, interest, decision, and action.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (19, 1, 10, N'Why is proper nutrition important?', 1, 5, N'Proper nutrition is essential for maintaining good health.')
INSERT [dbo].[Question] ([id], [question_type_id], [quiz_id], [title], [randomize], [points], [explanation]) VALUES (20, 2, 10, N'Name two essential nutrients and their functions.', 0, 10, N'Proteins for growth and repair, carbohydrates for energy.')
SET IDENTITY_INSERT [dbo].[Question] OFF
GO
SET IDENTITY_INSERT [dbo].[QuestionType] ON 

INSERT [dbo].[QuestionType] ([id], [type]) VALUES (1, N'Multiple Choice')
INSERT [dbo].[QuestionType] ([id], [type]) VALUES (2, N'True/False')
SET IDENTITY_INSERT [dbo].[QuestionType] OFF
GO
SET IDENTITY_INSERT [dbo].[Quiz] ON 

INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (1, N'Introduction to IT', N'Basic concepts of Information Technology.', 3, 70, CAST(N'00:30:00' AS Time), 1)
INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (2, N'UI/UX Fundamentals', N'Understanding the basics of UI/UX design.', 2, 75, CAST(N'00:45:00' AS Time), 2)
INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (3, N'Marketing Basics', N'Core principles of marketing.', 3, 60, CAST(N'01:00:00' AS Time), 3)
INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (4, N'Healthy Lifestyle', N'Tips for maintaining a healthy lifestyle.', 5, 80, CAST(N'00:20:00' AS Time), 4)
INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (5, N'Photography Techniques', N'Fundamentals of photography.', 4, 70, CAST(N'00:40:00' AS Time), 5)
INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (6, N'Video Production', N'Basic video production skills.', 3, 65, CAST(N'01:30:00' AS Time), 6)
INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (7, N'Advanced IT Concepts', N'In-depth IT topics.', 2, 75, CAST(N'01:00:00' AS Time), 1)
INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (8, N'UI/UX Advanced', N'Advanced UI/UX design techniques.', 2, 80, CAST(N'00:50:00' AS Time), 2)
INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (9, N'Marketing Strategies', N'Effective marketing strategies.', 3, 70, CAST(N'01:10:00' AS Time), 3)
INSERT [dbo].[Quiz] ([id], [name], [summary], [attempts_allowed], [passing_grade], [duration], [section_id]) VALUES (10, N'Nutrition and Wellness', N'Nutritional advice for better health.', 5, 85, CAST(N'00:25:00' AS Time), 4)
SET IDENTITY_INSERT [dbo].[Quiz] OFF
GO
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (11, 1, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 90, 1)
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (12, 2, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 80, 1)
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (13, 3, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 70, 1)
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (14, 4, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 60, 0)
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (15, 5, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 50, 0)
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (16, 6, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 90, 1)
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (7, 7, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 80, 1)
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (8, 8, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 70, 1)
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (9, 9, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 60, 0)
INSERT [dbo].[QuizResult] ([mentee_id], [quiz_id], [date], [mark], [result]) VALUES (10, 10, CAST(N'2024-07-11T22:37:28.220' AS DateTime), 50, 0)
GO
SET IDENTITY_INSERT [dbo].[Resource] ON 

INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (1, 1, 1)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (2, 2, 1)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (3, 3, 2)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (4, 4, 2)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (5, 5, 3)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (6, 6, 3)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (7, 7, 3)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (8, 8, 1)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (9, 9, 2)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (10, 10, 3)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (11, 11, 4)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (12, 12, 4)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (13, 13, 5)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (14, 14, 5)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (15, 15, 6)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (16, 16, 6)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (17, 17, 7)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (18, 18, 7)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (19, 19, 8)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (20, 20, 8)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (21, 21, 9)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (22, 22, 9)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (23, 23, 10)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (24, 24, 10)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (25, 25, 11)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (26, 26, 11)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (27, 27, 12)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (28, 28, 12)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (29, 29, 13)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (30, 30, 13)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (31, 31, 14)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (32, 32, 14)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (33, 33, 15)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (34, 34, 15)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (35, 35, 16)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (36, 36, 16)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (37, 37, 17)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (38, 38, 17)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (39, 39, 18)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (40, 40, 18)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (41, 41, 19)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (42, 42, 19)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (43, 43, 20)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (44, 44, 20)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (45, 45, 21)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (46, 46, 21)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (47, 47, 22)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (48, 48, 22)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (49, 49, 23)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (50, 50, 23)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (51, 51, 24)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (52, 52, 24)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (53, 53, 25)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (54, 54, 25)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (55, 55, 26)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (56, 56, 26)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (57, 57, 27)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (58, 58, 27)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (59, 59, 28)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (60, 60, 28)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (61, 61, 29)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (62, 62, 29)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (63, 63, 30)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (64, 64, 30)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (65, 65, 31)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (66, 66, 31)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (67, 67, 32)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (68, 68, 32)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (69, 69, 33)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (70, 70, 33)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (71, 71, 34)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (72, 72, 34)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (73, 73, 35)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (74, 74, 35)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (75, 75, 36)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (76, 76, 36)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (77, 77, 37)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (78, 78, 37)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (79, 79, 38)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (80, 80, 38)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (81, 81, 39)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (82, 82, 39)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (83, 83, 40)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (84, 84, 40)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (85, 85, 41)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (86, 86, 41)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (87, 87, 42)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (88, 88, 42)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (89, 89, 43)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (90, 90, 43)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (91, 91, 44)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (92, 92, 44)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (93, 93, 45)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (94, 94, 45)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (95, 95, 46)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (96, 96, 46)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (97, 97, 47)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (98, 98, 47)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (99, 99, 48)
GO
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (100, 100, 48)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (101, 101, 49)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (102, 102, 49)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (103, 103, 50)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (104, 104, 50)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (105, 105, 51)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (106, 106, 51)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (107, 107, 52)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (108, 108, 52)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (109, 109, 53)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (110, 110, 53)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (111, 111, 54)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (112, 112, 54)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (113, 113, 55)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (114, 114, 55)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (115, 115, 56)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (116, 116, 56)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (117, 117, 57)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (118, 118, 57)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (119, 119, 58)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (120, 120, 58)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (121, 121, 59)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (122, 122, 59)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (123, 123, 60)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (124, 124, 60)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (125, 125, 61)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (126, 126, 61)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (127, 127, 62)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (128, 128, 62)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (129, 129, 63)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (130, 130, 63)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (131, 131, 64)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (132, 132, 64)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (133, 133, 65)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (134, 134, 65)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (135, 135, 66)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (136, 136, 66)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (137, 137, 67)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (138, 138, 67)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (139, 139, 68)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (140, 140, 68)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (141, 141, 69)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (142, 142, 69)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (143, 143, 70)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (144, 144, 70)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (145, 145, 71)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (146, 146, 71)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (147, 147, 72)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (148, 148, 72)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (149, 149, 73)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (150, 150, 73)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (151, 151, 74)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (152, 152, 74)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (153, 153, 75)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (154, 154, 75)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (155, 155, 76)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (156, 156, 76)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (157, 157, 77)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (158, 158, 77)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (159, 159, 78)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (160, 160, 78)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (161, 161, 79)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (162, 162, 79)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (163, 163, 80)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (164, 164, 80)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (165, 165, 81)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (166, 166, 81)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (167, 167, 82)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (168, 168, 82)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (169, 169, 83)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (170, 170, 83)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (171, 171, 84)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (172, 172, 84)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (173, 173, 85)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (174, 174, 85)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (175, 175, 86)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (176, 176, 86)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (177, 177, 87)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (178, 178, 87)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (179, 179, 88)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (180, 180, 88)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (181, 181, 89)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (182, 182, 89)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (183, 183, 90)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (184, 184, 90)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (185, 185, 91)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (186, 186, 91)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (187, 187, 92)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (188, 188, 92)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (189, 189, 93)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (190, 190, 93)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (191, 191, 94)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (192, 192, 94)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (193, 193, 95)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (194, 194, 95)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (195, 195, 96)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (196, 196, 96)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (197, 197, 97)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (198, 198, 97)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (199, 199, 98)
GO
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (200, 200, 98)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (201, 201, 99)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (202, 202, 99)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (203, 203, 100)
INSERT [dbo].[Resource] ([id], [asset_id], [lesson_id]) VALUES (204, 204, 100)
SET IDENTITY_INSERT [dbo].[Resource] OFF
GO
SET IDENTITY_INSERT [dbo].[Review] ON 

INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (1, 11, 7, 1, 4, N'Python course was informative, enjoyed learning!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (2, 12, 8, 1, 3, N'UI/UX design principles were interesting but complex.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (3, 13, 9, 1, 5, N'Digital marketing strategies were spot on, very practical.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (4, 14, 10, 1, 4, N'Healthy lifestyle habits course was motivating and helpful.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (5, 15, 11, 1, 5, N'Photography masterclass exceeded my expectations!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (6, 16, 12, 1, 4, N'Video production essentials course was well-structured.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (7, 17, 13, 1, 3, N'Data structures in C++ were challenging but rewarding.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (8, 18, 14, 1, 5, N'Introduction to web development was a great starting point.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (9, 19, 15, 1, 4, N'Effective communication skills course improved my interactions.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (10, 20, 16, 1, 5, N'Financial planning and budgeting course was practical and useful.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (11, 1, 11, 1, 5, N'Excellent course, very informative and well-structured.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (12, 2, 12, 1, 4, N'Great insights on UI/UX design principles.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (13, 3, 13, 1, 3, N'Good content but could be more detailed.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (14, 4, 14, 1, 5, N'Practical tips for a healthy lifestyle, highly recommended!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (15, 5, 15, 1, 4, N'Learned a lot about photography techniques.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (16, 6, 7, 1, 5, N'Fantastic video production course!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (17, 7, 8, 1, 4, N'Advanced concepts explained clearly.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (18, 8, 9, 1, 3, N'Good introduction to web development.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (19, 9, 10, 1, 5, N'Effective communication skills explained well.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (20, 10, 15, 1, 4, N'Useful financial planning and budgeting tips.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (21, 21, 7, 1, 4, N'Learning SQL was essential for my career development.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (22, 22, 8, 1, 5, N'Web accessibility course taught me a lot about inclusivity.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (23, 23, 9, 1, 3, N'Design thinking course was interesting but lacked practical examples.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (24, 24, 10, 1, 4, N'SEO best practices course was informative and well-structured.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (25, 25, 11, 1, 5, N'Healthy eating habits course changed my lifestyle positively.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (26, 26, 12, 1, 4, N'Landscape photography course improved my photography skills.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (27, 27, 13, 1, 3, N'Film production basics course covered essential concepts well.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (28, 28, 14, 1, 5, N'Introduction to SQL course provided a solid foundation in databases.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (29, 29, 15, 1, 4, N'User experience research course enhanced my design research skills.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (30, 30, 16, 1, 5, N'Content marketing strategies course helped me refine my marketing skills.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (31, 11, 7, 1, 4, N'Python course was informative, enjoyed learning!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (32, 12, 8, 1, 3, N'UI/UX design principles were interesting but complex.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (33, 13, 9, 1, 5, N'Digital marketing strategies were spot on, very practical.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (34, 14, 10, 1, 4, N'Healthy lifestyle habits course was motivating and helpful.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (35, 15, 11, 1, 5, N'Photography masterclass exceeded my expectations!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (36, 16, 12, 1, 4, N'Video production essentials course was well-structured.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (37, 17, 13, 1, 3, N'Data structures in C++ were challenging but rewarding.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (38, 18, 14, 1, 5, N'Introduction to web development was a great starting point.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (39, 19, 15, 1, 4, N'Effective communication skills course improved my interactions.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (40, 20, 16, 1, 5, N'Financial planning and budgeting course was practical and useful.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (41, 1, 11, 1, 5, N'Excellent course, very informative and well-structured.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (42, 2, 12, 1, 4, N'Great insights on UI/UX design principles.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (43, 3, 13, 1, 3, N'Good content but could be more detailed.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (44, 4, 14, 1, 5, N'Practical tips for a healthy lifestyle, highly recommended!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (45, 5, 15, 1, 4, N'Learned a lot about photography techniques.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (46, 6, 7, 1, 5, N'Fantastic video production course!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (47, 7, 8, 1, 4, N'Advanced concepts explained clearly.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (48, 8, 9, 1, 3, N'Good introduction to web development.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (49, 9, 10, 1, 5, N'Effective communication skills explained well.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (50, 10, 15, 1, 4, N'Useful financial planning and budgeting tips.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (51, 21, 7, 1, 4, N'Learning SQL was essential for my career development.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (52, 22, 8, 1, 5, N'Web accessibility course taught me a lot about inclusivity.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (53, 23, 9, 1, 3, N'Design thinking course was interesting but lacked practical examples.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (54, 24, 10, 1, 4, N'SEO best practices course was informative and well-structured.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (55, 25, 11, 1, 5, N'Healthy eating habits course changed my lifestyle positively.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (56, 26, 12, 1, 4, N'Landscape photography course improved my photography skills.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (57, 27, 13, 1, 3, N'Film production basics course covered essential concepts well.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (58, 28, 14, 1, 5, N'Introduction to SQL course provided a solid foundation in databases.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (59, 29, 15, 1, 4, N'User experience research course enhanced my design research skills.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (60, 30, 16, 1, 5, N'Content marketing strategies course helped me refine my marketing skills.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (61, 31, 7, 1, 4, N'Flutter course was insightful and practical.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (62, 32, 8, 1, 3, N'DevOps principles were interesting but complex.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (63, 33, 9, 1, 5, N'Blockchain technology was explained well.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (64, 34, 10, 1, 4, N'Machine learning concepts were challenging and informative.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (65, 35, 11, 1, 5, N'Cloud computing course provided valuable insights.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (66, 36, 12, 1, 4, N'Cybersecurity practices were practical and useful.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (67, 37, 13, 1, 3, N'Artificial intelligence course covered advanced topics.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (68, 38, 14, 1, 5, N'Project management course was well-structured.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (69, 39, 15, 1, 4, N'UX design course enhanced my design skills.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (70, 40, 16, 1, 5, N'React course was excellent, learned a lot about frontend development.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (71, 11, 7, 2, 4, N'Python course was informative, enjoyed learning!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (72, 12, 8, 2, 3, N'UI/UX design principles were interesting but complex.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (73, 13, 9, 2, 5, N'Digital marketing strategies were spot on, very practical.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (74, 14, 10, 2, 4, N'Healthy lifestyle habits course was motivating and helpful.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (75, 15, 11, 2, 5, N'Photography masterclass exceeded my expectations!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (76, 6, 12, 2, 4, N'Video production essentials course was well-structured.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (77, 7, 13, 2, 3, N'Data structures in C++ were challenging but rewarding.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (78, 8, 14, 2, 5, N'Introduction to web development was a great starting point.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (79, 9, 15, 2, 4, N'Effective communication skills course improved my interactions.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (80, 10, 16, 2, 5, N'Financial planning and budgeting course was practical and useful.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (81, 1, 11, 2, 5, N'Excellent course, very informative and well-structured.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (82, 2, 12, 3, 4, N'Great insights on UI/UX design principles.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (83, 3, 13, 3, 3, N'Good content but could be more detailed.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (84, 4, 14, 3, 5, N'Practical tips for a healthy lifestyle, highly recommended!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (85, 5, 15, 3, 4, N'Learned a lot about photography techniques.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (86, 6, 7, 3, 5, N'Fantastic video production course!', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (87, 7, 8, 3, 4, N'Advanced concepts explained clearly.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (88, 8, 9, 3, 3, N'Good introduction to web development.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (89, 9, 10, 3, 5, N'Effective communication skills explained well.', CAST(N'22:37:28.2033333' AS Time))
INSERT [dbo].[Review] ([id], [source_id], [user_id], [source_type_id], [rating_star], [content], [review_at]) VALUES (90, 10, 15, 3, 4, N'Useful financial planning and budgeting tips.', CAST(N'22:37:28.2033333' AS Time))
SET IDENTITY_INSERT [dbo].[Review] OFF
GO
SET IDENTITY_INSERT [dbo].[Role] ON 

INSERT [dbo].[Role] ([id], [name]) VALUES (1, N'mentee')
INSERT [dbo].[Role] ([id], [name]) VALUES (2, N'mentor')
INSERT [dbo].[Role] ([id], [name]) VALUES (3, N'admin')
SET IDENTITY_INSERT [dbo].[Role] OFF
GO
SET IDENTITY_INSERT [dbo].[Section] ON 

INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (1, N'Introduction', 1)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (2, N'Basic Concepts', 1)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (3, N'Advanced Techniques', 1)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (4, N'Introduction to UI/UX', 2)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (5, N'Design Basics', 2)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (6, N'Advanced UI/UX Techniques', 2)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (7, N'Introduction to Digital Marketing', 3)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (8, N'Marketing Fundamentals', 3)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (9, N'Advanced Marketing Strategies', 3)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (10, N'Introduction to Healthy Lifestyle', 4)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (11, N'Healthy Eating', 4)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (12, N'Exercise and Fitness', 4)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (13, N'Introduction to Photography', 5)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (14, N'Photography Techniques', 5)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (15, N'Advanced Photography', 5)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (16, N'Introduction to Video Production', 6)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (17, N'Video Editing Basics', 6)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (18, N'Advanced Video Production', 6)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (19, N'Introduction to Data Structures', 7)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (20, N'Intermediate Data Structures', 7)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (21, N'Advanced Data Structures', 7)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (22, N'Introduction to Web Development', 8)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (23, N'HTML and CSS Basics', 8)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (24, N'JavaScript Fundamentals', 8)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (25, N'Introduction to Communication Skills', 9)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (26, N'Verbal Communication', 9)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (27, N'Non-verbal Communication', 9)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (28, N'Introduction to Financial Planning', 10)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (29, N'Budgeting Basics', 10)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (30, N'Advanced Financial Strategies', 10)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (31, N'Introduction to Data Science', 11)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (32, N'R Programming Basics', 11)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (33, N'Advanced Data Science Techniques', 11)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (34, N'Introduction to Graphic Design', 12)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (35, N'Design Tools', 12)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (36, N'Advanced Graphic Design', 12)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (37, N'Introduction to Social Media Marketing', 13)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (38, N'Marketing Strategies', 13)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (39, N'Advanced Social Media Techniques', 13)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (40, N'Introduction to Personal Development', 14)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (41, N'Wellness Techniques', 14)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (42, N'Advanced Personal Development', 14)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (43, N'Introduction to Advanced Photography', 15)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (44, N'Photography Tools', 15)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (45, N'Professional Photography Techniques', 15)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (46, N'Introduction to Video Editing', 16)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (47, N'Editing Tools', 16)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (48, N'Advanced Editing Techniques', 16)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (49, N'Introduction to Machine Learning', 17)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (50, N'Python for Machine Learning', 17)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (51, N'Advanced Machine Learning', 17)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (52, N'Introduction to User Experience', 18)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (53, N'Research Methods', 18)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (54, N'Advanced UX Techniques', 18)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (55, N'Introduction to Content Marketing', 19)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (56, N'Content Creation', 19)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (57, N'Advanced Marketing Strategies', 19)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (58, N'Introduction to Mindfulness', 20)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (59, N'Meditation Techniques', 20)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (60, N'Advanced Mindfulness', 20)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (61, N'Introduction to Portrait Photography', 21)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (62, N'Photography Techniques', 21)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (63, N'Advanced Portrait Photography', 21)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (64, N'Introduction to Videography', 22)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (65, N'Videography Tools', 22)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (66, N'Professional Videography Techniques', 22)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (67, N'Introduction to Data Analysis', 23)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (68, N'Excel Tools', 23)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (69, N'Advanced Data Analysis', 23)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (70, N'Introduction to Design Thinking', 24)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (71, N'Design Thinking Methods', 24)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (72, N'Advanced Design Thinking', 24)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (73, N'Introduction to SEO', 25)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (74, N'SEO Tools', 25)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (75, N'Advanced SEO Techniques', 25)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (76, N'Introduction to Healthy Eating', 26)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (77, N'Nutrition Basics', 26)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (78, N'Advanced Healthy Eating', 26)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (79, N'Introduction to Landscape Photography', 27)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (80, N'Photography Techniques', 27)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (81, N'Advanced Landscape Photography', 27)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (82, N'Introduction to Film Production', 28)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (83, N'Film Production Tools', 28)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (84, N'Advanced Film Production', 28)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (85, N'Introduction to SQL', 29)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (86, N'SQL Basics', 29)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (87, N'Advanced SQL Techniques', 29)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (88, N'Introduction to Web Accessibility', 30)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (89, N'Accessibility Tools', 30)
INSERT [dbo].[Section] ([id], [name], [course_id]) VALUES (90, N'Advanced Accessibility Techniques', 30)
SET IDENTITY_INSERT [dbo].[Section] OFF
GO
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (1, N'SourceType', N'course', 1)
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (2, N'SourceType', N'challenge', 2)
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (3, N'SourceType', N'program', 3)
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (4, N'Role', N'Admin', 1)
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (5, N'Role', N'Mentor', 2)
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (6, N'Role', N'Mentee', 3)
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (7, N'Criteria', N'Enrollments', 35)
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (8, N'Criteria', N'Completion Rate', 35)
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (9, N'Criteria', N'Average Learner Rating', 30)
INSERT [dbo].[Setting] ([id], [setting_type], [setting_name], [setting_value]) VALUES (10, N'Criteria', N'New Mentee', 30)
GO
INSERT [dbo].[Skill] ([id], [name]) VALUES (1, N'Design Software')
INSERT [dbo].[Skill] ([id], [name]) VALUES (2, N'Research')
INSERT [dbo].[Skill] ([id], [name]) VALUES (3, N'User Experience')
INSERT [dbo].[Skill] ([id], [name]) VALUES (4, N'User Interface Design')
GO
SET IDENTITY_INSERT [dbo].[SourceImage] ON 

INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (1, 1, 101, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (2, 2, 102, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (3, 3, 103, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (4, 4, 104, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (5, 5, 105, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (6, 6, 106, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (7, 7, 107, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (8, 8, 108, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (9, 9, 109, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (10, 10, 110, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (11, 11, 111, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (12, 12, 112, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (13, 13, 113, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (14, 14, 114, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (15, 15, 115, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (16, 16, 116, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (17, 17, 117, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (18, 18, 118, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (19, 19, 119, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (20, 20, 120, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (21, 21, 121, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (22, 22, 122, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (23, 23, 123, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (24, 24, 124, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (25, 25, 125, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (26, 26, 126, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (27, 27, 127, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (28, 28, 128, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (29, 29, 129, 1)
INSERT [dbo].[SourceImage] ([id], [source_id], [asset_id], [source_type_id]) VALUES (30, 30, 130, 1)
SET IDENTITY_INSERT [dbo].[SourceImage] OFF
GO
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (1, 2, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (1, 2, 5)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (1, 3, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (2, 2, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (2, 2, 6)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (2, 3, 2)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (2, 3, 11)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 2, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 2, 5)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 2, 6)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 2, 7)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 2, 8)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 2, 9)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 3, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 3, 5)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 3, 6)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 3, 7)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 3, 8)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (3, 3, 9)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (4, 2, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (4, 2, 5)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (4, 2, 6)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (4, 3, 18)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (5, 2, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (5, 2, 5)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (5, 2, 6)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (5, 3, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (6, 2, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (6, 2, 5)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (6, 2, 7)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (6, 3, 2)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (6, 3, 11)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (7, 2, 11)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (7, 3, 12)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (8, 2, 19)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (8, 2, 20)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (8, 3, 13)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (9, 2, 3)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (9, 3, 14)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (10, 2, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (10, 3, 15)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (10, 3, 16)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (11, 2, 5)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (11, 3, 17)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (12, 2, 6)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (12, 3, 18)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (13, 2, 4)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (13, 2, 5)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (13, 3, 19)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (14, 2, 19)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (14, 3, 20)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (15, 2, 6)
INSERT [dbo].[SourceTag] ([source_id], [source_type_id], [tag_id]) VALUES (15, 3, 21)
GO
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (1, 1, 4, 1)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (2, 2, 3, 3)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (3, 3, 4, 3)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (4, 5, 1, 2)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (5, 4, 5, 1)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (6, 6, 5, 1)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (7, 7, 5, 2)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (8, 8, 4, 3)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (9, 9, 2, 3)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (10, 10, 2, 2)
INSERT [dbo].[SourceTemplate] ([id], [template_id], [source_id], [sourcetype_id]) VALUES (11, 11, 2, 2)
GO
SET IDENTITY_INSERT [dbo].[StatusMessage] ON 

INSERT [dbo].[StatusMessage] ([id], [name]) VALUES (1, N'Sent')
INSERT [dbo].[StatusMessage] ([id], [name]) VALUES (2, N'Delivered')
INSERT [dbo].[StatusMessage] ([id], [name]) VALUES (3, N'Read')
SET IDENTITY_INSERT [dbo].[StatusMessage] OFF
GO
SET IDENTITY_INSERT [dbo].[Subsystem] ON 

INSERT [dbo].[Subsystem] ([id], [name], [description], [created_at]) VALUES (1, N'Communication', N'Communication Subsystem', CAST(N'2024-07-18T06:05:13.767' AS DateTime))
INSERT [dbo].[Subsystem] ([id], [name], [description], [created_at]) VALUES (2, N'Course Management', N'Course Management Subsystem', CAST(N'2024-07-18T06:05:13.767' AS DateTime))
INSERT [dbo].[Subsystem] ([id], [name], [description], [created_at]) VALUES (3, N'Mentoring Hub', N'Mentoring Hub', CAST(N'2024-07-18T06:05:13.767' AS DateTime))
SET IDENTITY_INSERT [dbo].[Subsystem] OFF
GO
SET IDENTITY_INSERT [dbo].[Tag] ON 

INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (1, N'Python')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (2, N'Data Science')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (3, N'Selenium')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (4, N'Web Development')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (5, N'React')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (6, N'React Router')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (7, N'Redux')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (8, N'NextJS')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (9, N'React Native')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (10, N'Jupyter Notebook')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (11, N'Machine Learning')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (12, N'Cloud Computing')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (13, N'Cybersecurity')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (14, N'Java')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (15, N'Blockchain')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (16, N'Cryptocurrency')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (17, N'Artificial Intelligence')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (18, N'Project Management')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (19, N'UX Design')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (20, N'Flutter')
INSERT [dbo].[Tag] ([id], [tag_name]) VALUES (21, N'DevOps')
SET IDENTITY_INSERT [dbo].[Tag] OFF
GO
INSERT [dbo].[TotalMember] ([total_member]) VALUES (9)
GO
INSERT [dbo].[University] ([id], [name], [img]) VALUES (1, N'HCMC University of Technology and Education', N'link')
INSERT [dbo].[University] ([id], [name], [img]) VALUES (2, N'Harvard University', N'link')
INSERT [dbo].[University] ([id], [name], [img]) VALUES (3, N'Boston University', N'link')
GO
SET IDENTITY_INSERT [dbo].[User] ON 

INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (1, N'John Doe', 1, 1, 1, 1, CAST(N'2024-07-01T08:00:00.000' AS DateTime), 40, N'Male', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (2, N'Alice Smith', 2, 2, 2, 2, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 35, N'Female', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (3, N'Bob Johnson', 3, 3, 3, 2, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 36, N'Male', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (4, N'Carol White', 4, 4, 4, 2, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 37, N'Female', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (5, N'David Brown', 5, 1, 5, 2, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 38, N'Male', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (6, N'Eve Black', 6, 2, 1, 2, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 39, N'Female', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (7, N'Frank Green', 7, 3, 2, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 20, N'Male', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (8, N'Grace Lee', 8, 4, 3, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 21, N'Female', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (9, N'Hank Martin', 9, 1, 4, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 22, N'Male', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (10, N'Ivy Clark', 10, 2, 5, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 23, N'Female', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (11, N'Jack Walker', 11, 3, 1, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 24, N'Male', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (12, N'Kara Adams', 12, 4, 2, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 25, N'Female', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (13, N'Liam Young', 13, 1, 3, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 26, N'Male', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (14, N'Mia King', 14, 2, 4, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 27, N'Female', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (15, N'Noah Scott', 15, 3, 5, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 28, N'Male', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (16, N'Olivia Baker', 16, 4, 1, 3, CAST(N'2024-07-07T08:00:00.000' AS DateTime), 29, N'Female', 1, NULL, NULL)
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (17, N'Jaquelin Heathcote', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'zleffler@example.com')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (18, N'Mr. Abdiel Zemlak II', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'brian59@example.com')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (19, N'Dr. Clementine Rice', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'jaquan94@example.com')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (20, N'Whitney Reilly', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'brook64@example.net')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (21, N'Merl Renner', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'lynch.daisy@example.com')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (22, N'Annabell Welch', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'jerome.mccullough@example.com')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (23, N'Miss Nadia Wilkinson MD', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'eusebio.cartwright@example.org')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (24, N'Tessie Beahan', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'megane42@example.net')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (25, N'Maximillian Lynch', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'tfahey@example.org')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (26, N'Jayson Walker', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'christiansen.nico@example.org')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (27, N'Misty Carter V', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'ehegmann@example.com')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (28, N'Arturo Johns IV', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'harber.kiera@example.com')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (29, N'Prof. Torey Hammes', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'zaria19@example.org')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (30, N'Izaiah Murazik IV', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'dion.muller@example.org')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (31, N'Dr. Erwin Weber', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'blair54@example.com')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (32, N'Miss Alexandrea Howe', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'wanda.herman@example.net')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (33, N'Lowell Denesik', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'pmuller@example.com')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (34, N'Prof. Ryley Mante V', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'aubree.emard@example.org')
INSERT [dbo].[User] ([id], [name], [asset_id], [location_id], [jobtitle_id], [role_id], [create_at], [age], [gender], [status], [dob], [email]) VALUES (35, N'Dr. Donnie Erdman MD', NULL, NULL, NULL, NULL, CAST(N'2024-07-17T08:38:27.950' AS DateTime), NULL, NULL, NULL, CAST(N'2024-07-17' AS Date), N'sallie.crist@example.com')
SET IDENTITY_INSERT [dbo].[User] OFF
GO
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (7, CAST(N'2023-06-01' AS Date), CAST(N'01:00:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (7, CAST(N'2023-06-01' AS Date), CAST(N'00:30:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (7, CAST(N'2023-06-01' AS Date), CAST(N'00:45:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (8, CAST(N'2023-06-01' AS Date), CAST(N'01:00:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (8, CAST(N'2023-06-01' AS Date), CAST(N'00:30:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (8, CAST(N'2023-06-01' AS Date), CAST(N'00:45:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (11, CAST(N'2023-06-01' AS Date), CAST(N'01:00:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (11, CAST(N'2023-06-01' AS Date), CAST(N'00:30:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (11, CAST(N'2023-06-01' AS Date), CAST(N'00:45:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (12, CAST(N'2023-06-01' AS Date), CAST(N'01:15:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (12, CAST(N'2023-06-01' AS Date), CAST(N'00:50:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (12, CAST(N'2023-06-01' AS Date), CAST(N'01:30:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (13, CAST(N'2023-06-01' AS Date), CAST(N'00:30:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (13, CAST(N'2023-06-01' AS Date), CAST(N'01:00:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (13, CAST(N'2023-06-01' AS Date), CAST(N'02:00:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (14, CAST(N'2023-06-01' AS Date), CAST(N'00:45:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (14, CAST(N'2023-06-01' AS Date), CAST(N'01:30:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (14, CAST(N'2023-06-01' AS Date), CAST(N'01:00:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (15, CAST(N'2023-06-01' AS Date), CAST(N'00:50:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (15, CAST(N'2023-06-01' AS Date), CAST(N'01:15:00' AS Time))
INSERT [dbo].[UserOnline] ([user_id], [online_date], [online_time]) VALUES (15, CAST(N'2023-06-01' AS Date), CAST(N'00:45:00' AS Time))
GO
SET IDENTITY_INSERT [dbo].[UserPaymentInfo] ON 

INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (1, 11, N'John Doe', N'4111111111111111', CAST(N'2025-12-31T00:00:00.000' AS DateTime), 1)
INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (2, 12, N'Jane Smith', N'4222222222222222', CAST(N'2024-11-30T00:00:00.000' AS DateTime), 2)
INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (3, 13, N'Michael Johnson', N'4333333333333333', CAST(N'2026-10-31T00:00:00.000' AS DateTime), 3)
INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (4, 14, N'Emily Brown', N'4444444444444444', CAST(N'2023-09-30T00:00:00.000' AS DateTime), 4)
INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (5, 15, N'David Wilson', N'4555555555555555', CAST(N'2027-08-31T00:00:00.000' AS DateTime), 5)
INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (6, 16, N'Sarah Lee', N'4666666666666666', CAST(N'2025-07-31T00:00:00.000' AS DateTime), 4)
INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (7, 7, N'Chris Martin', N'4777777777777777', CAST(N'2023-06-30T00:00:00.000' AS DateTime), 2)
INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (8, 8, N'Jessica Taylor', N'4888888888888888', CAST(N'2024-05-31T00:00:00.000' AS DateTime), 1)
INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (9, 9, N'Brian Harris', N'4999999999999999', CAST(N'2026-04-30T00:00:00.000' AS DateTime), 3)
INSERT [dbo].[UserPaymentInfo] ([id], [user_id], [name_on_card], [card_number], [expiry_date], [payment_method_id]) VALUES (10, 10, N'Laura Clark', N'4000000000000000', CAST(N'2027-03-31T00:00:00.000' AS DateTime), 2)
SET IDENTITY_INSERT [dbo].[UserPaymentInfo] OFF
GO
INSERT [dbo].[UserSkill] ([id], [user_id], [skill_id]) VALUES (1, 1, 3)
INSERT [dbo].[UserSkill] ([id], [user_id], [skill_id]) VALUES (2, 1, 4)
INSERT [dbo].[UserSkill] ([id], [user_id], [skill_id]) VALUES (3, 2, 1)
GO
SET IDENTITY_INSERT [dbo].[Voucher] ON 

INSERT [dbo].[Voucher] ([id], [code], [source_id], [source_type_id], [discount], [quantity], [expire_date]) VALUES (1, N'DISCOUNT10', 1, 3, 10, 100, CAST(N'2024-12-31T23:59:59.000' AS DateTime))
INSERT [dbo].[Voucher] ([id], [code], [source_id], [source_type_id], [discount], [quantity], [expire_date]) VALUES (2, N'SAVE20', 2, 3, 20, 50, CAST(N'2024-11-30T23:59:59.000' AS DateTime))
INSERT [dbo].[Voucher] ([id], [code], [source_id], [source_type_id], [discount], [quantity], [expire_date]) VALUES (3, N'OFFER30', 3, 3, 30, 25, CAST(N'2024-10-31T23:59:59.000' AS DateTime))
INSERT [dbo].[Voucher] ([id], [code], [source_id], [source_type_id], [discount], [quantity], [expire_date]) VALUES (4, N'PROMO15', 4, 3, 15, 200, CAST(N'2024-09-30T23:59:59.000' AS DateTime))
INSERT [dbo].[Voucher] ([id], [code], [source_id], [source_type_id], [discount], [quantity], [expire_date]) VALUES (5, N'DEAL25', 5, 2, 25, 75, CAST(N'2024-08-31T23:59:59.000' AS DateTime))
SET IDENTITY_INSERT [dbo].[Voucher] OFF
GO
INSERT [dbo].[WorkingType] ([id], [name]) VALUES (1, N'Fulltime')
INSERT [dbo].[WorkingType] ([id], [name]) VALUES (2, N'Partime')
INSERT [dbo].[WorkingType] ([id], [name]) VALUES (3, N'Online Program')
GO
SET IDENTITY_INSERT [dbo].[Workspace] ON 

INSERT [dbo].[Workspace] ([id], [name], [owner_id], [source_id], [source_type_id]) VALUES (1, N'Workspace 1', 1, NULL, NULL)
INSERT [dbo].[Workspace] ([id], [name], [owner_id], [source_id], [source_type_id]) VALUES (2, N'Workspace 2', 2, NULL, NULL)
INSERT [dbo].[Workspace] ([id], [name], [owner_id], [source_id], [source_type_id]) VALUES (3, N'Workspace 3', 3, 1, 1)
SET IDENTITY_INSERT [dbo].[Workspace] OFF
GO
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (1, 1, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (1, 2, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (1, 3, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (1, 4, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (1, 5, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (1, 6, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (1, 7, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (2, 1, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (2, 2, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (2, 3, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (3, 1, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (3, 2, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
INSERT [dbo].[WorkspaceMember] ([workspace_id], [user_id], [join_at], [updated_at], [left_at], [role_id]) VALUES (3, 3, CAST(N'2024-07-18T06:05:13.853' AS DateTime), CAST(N'2024-07-18T06:05:13.853' AS DateTime), NULL, NULL)
GO
ALTER TABLE [dbo].[Channel] ADD  DEFAULT ((1)) FOR [is_private]
GO
ALTER TABLE [dbo].[ChannelPrivateMember] ADD  DEFAULT (NULL) FOR [role_id]
GO
ALTER TABLE [dbo].[Feedback] ADD  DEFAULT (NULL) FOR [group_id]
GO
ALTER TABLE [dbo].[Feedback] ADD  DEFAULT (NULL) FOR [updated_at]
GO
ALTER TABLE [dbo].[MeetingParticipant] ADD  DEFAULT (NULL) FOR [joined_at]
GO
ALTER TABLE [dbo].[MeetingParticipant] ADD  DEFAULT (NULL) FOR [left_at]
GO
ALTER TABLE [dbo].[Message] ADD  DEFAULT (NULL) FOR [channel_id]
GO
ALTER TABLE [dbo].[Message] ADD  DEFAULT (NULL) FOR [dms_id]
GO
ALTER TABLE [dbo].[Message] ADD  DEFAULT (NULL) FOR [parent_id]
GO
ALTER TABLE [dbo].[Message] ADD  DEFAULT (NULL) FOR [meeting_id]
GO
ALTER TABLE [dbo].[Message] ADD  DEFAULT (NULL) FOR [status_id]
GO
ALTER TABLE [dbo].[Message] ADD  DEFAULT (NULL) FOR [edited_at]
GO
ALTER TABLE [dbo].[Message] ADD  DEFAULT ((0)) FOR [is_deleted]
GO
ALTER TABLE [dbo].[Message] ADD  DEFAULT (NULL) FOR [deleted_at]
GO
ALTER TABLE [dbo].[NotificationQueue] ADD  DEFAULT ((0)) FOR [is_read]
GO
ALTER TABLE [dbo].[NotificationSetting] ADD  DEFAULT ((1)) FOR [enable]
GO
ALTER TABLE [dbo].[Preference] ADD  DEFAULT ((0)) FOR [dark_mode]
GO
ALTER TABLE [dbo].[User] ADD  DEFAULT (NULL) FOR [dob]
GO
ALTER TABLE [dbo].[Workspace] ADD  DEFAULT (NULL) FOR [source_id]
GO
ALTER TABLE [dbo].[WorkspaceMember] ADD  DEFAULT (NULL) FOR [left_at]
GO
ALTER TABLE [dbo].[WorkspaceMember] ADD  DEFAULT (NULL) FOR [role_id]
GO
ALTER TABLE [dbo].[BlockList]  WITH CHECK ADD FOREIGN KEY([dms_id])
REFERENCES [dbo].[DirectMessage] ([id])
GO
ALTER TABLE [dbo].[BlockList]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[BlockList]  WITH CHECK ADD FOREIGN KEY([user_id_is_blocked])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[Channel]  WITH CHECK ADD FOREIGN KEY([workspace_id])
REFERENCES [dbo].[Workspace] ([id])
GO
ALTER TABLE [dbo].[ChannelPrivateMember]  WITH CHECK ADD FOREIGN KEY([channel_id])
REFERENCES [dbo].[Channel] ([id])
GO
ALTER TABLE [dbo].[ChannelPrivateMember]  WITH CHECK ADD FOREIGN KEY([role_id])
REFERENCES [dbo].[Role] ([id])
GO
ALTER TABLE [dbo].[ChannelPrivateMember]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[ChannelShared]  WITH CHECK ADD FOREIGN KEY([channel_id])
REFERENCES [dbo].[Channel] ([id])
GO
ALTER TABLE [dbo].[ChannelShared]  WITH CHECK ADD FOREIGN KEY([original_workspace_id])
REFERENCES [dbo].[Workspace] ([id])
GO
ALTER TABLE [dbo].[ChannelShared]  WITH CHECK ADD FOREIGN KEY([target_workspace_id])
REFERENCES [dbo].[Workspace] ([id])
GO
ALTER TABLE [dbo].[DirectMessage]  WITH CHECK ADD FOREIGN KEY([user1])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[DirectMessage]  WITH CHECK ADD FOREIGN KEY([user2])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[EventParameter]  WITH CHECK ADD FOREIGN KEY([event_type_id])
REFERENCES [dbo].[EventTypeMess] ([id])
GO
ALTER TABLE [dbo].[Feedback]  WITH CHECK ADD FOREIGN KEY([group_id])
REFERENCES [dbo].[FeedbackGroup] ([id])
GO
ALTER TABLE [dbo].[Feedback]  WITH CHECK ADD FOREIGN KEY([status_id])
REFERENCES [dbo].[FeedbackStatus] ([id])
GO
ALTER TABLE [dbo].[Feedback]  WITH CHECK ADD FOREIGN KEY([subsystem_id])
REFERENCES [dbo].[Subsystem] ([id])
GO
ALTER TABLE [dbo].[Feedback]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[FeedbackAssignee]  WITH CHECK ADD FOREIGN KEY([assignee_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[FeedbackAssignee]  WITH CHECK ADD FOREIGN KEY([feedback_id])
REFERENCES [dbo].[Feedback] ([id])
GO
ALTER TABLE [dbo].[FeedbackResult]  WITH CHECK ADD FOREIGN KEY([feedback_id])
REFERENCES [dbo].[Feedback] ([id])
GO
ALTER TABLE [dbo].[FeedbackResultReply]  WITH CHECK ADD FOREIGN KEY([feedback_result_id])
REFERENCES [dbo].[FeedbackResult] ([id])
GO
ALTER TABLE [dbo].[FeedbackResultReply]  WITH CHECK ADD FOREIGN KEY([replied_by])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[Log]  WITH CHECK ADD FOREIGN KEY([event_type_id])
REFERENCES [dbo].[EventTypeMess] ([id])
GO
ALTER TABLE [dbo].[Log]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[LogDetail]  WITH CHECK ADD FOREIGN KEY([event_parameter_id])
REFERENCES [dbo].[EventParameter] ([id])
GO
ALTER TABLE [dbo].[LogDetail]  WITH CHECK ADD FOREIGN KEY([log_id])
REFERENCES [dbo].[Log] ([id])
GO
ALTER TABLE [dbo].[Meeting]  WITH CHECK ADD FOREIGN KEY([owner_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[MeetingParticipant]  WITH CHECK ADD FOREIGN KEY([meeting_id])
REFERENCES [dbo].[Meeting] ([id])
GO
ALTER TABLE [dbo].[MeetingParticipant]  WITH CHECK ADD FOREIGN KEY([status_id])
REFERENCES [dbo].[MeetingParticipantStatus] ([id])
GO
ALTER TABLE [dbo].[MeetingParticipant]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[Message]  WITH CHECK ADD FOREIGN KEY([channel_id])
REFERENCES [dbo].[Channel] ([id])
GO
ALTER TABLE [dbo].[Message]  WITH CHECK ADD FOREIGN KEY([dms_id])
REFERENCES [dbo].[DirectMessage] ([id])
GO
ALTER TABLE [dbo].[Message]  WITH CHECK ADD FOREIGN KEY([meeting_id])
REFERENCES [dbo].[Meeting] ([id])
GO
ALTER TABLE [dbo].[Message]  WITH CHECK ADD FOREIGN KEY([parent_id])
REFERENCES [dbo].[Message] ([id])
GO
ALTER TABLE [dbo].[Message]  WITH CHECK ADD FOREIGN KEY([sender_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[Message]  WITH CHECK ADD FOREIGN KEY([status_id])
REFERENCES [dbo].[StatusMessage] ([id])
GO
ALTER TABLE [dbo].[MessageAttachment]  WITH CHECK ADD FOREIGN KEY([message_id])
REFERENCES [dbo].[Message] ([id])
GO
ALTER TABLE [dbo].[MessageMention]  WITH CHECK ADD FOREIGN KEY([message_id])
REFERENCES [dbo].[Message] ([id])
GO
ALTER TABLE [dbo].[MessageMention]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[MessageReaction]  WITH CHECK ADD FOREIGN KEY([emoji_id])
REFERENCES [dbo].[Emoji] ([id])
GO
ALTER TABLE [dbo].[MessageReaction]  WITH CHECK ADD FOREIGN KEY([message_id])
REFERENCES [dbo].[Message] ([id])
GO
ALTER TABLE [dbo].[MessageReaction]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[NavigationBar]  WITH CHECK ADD FOREIGN KEY([feature_nav_bar])
REFERENCES [dbo].[MainFeature] ([id])
GO
ALTER TABLE [dbo].[NavigationBar]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[NotificationQueue]  WITH CHECK ADD FOREIGN KEY([notification_type_id])
REFERENCES [dbo].[NotificationType] ([id])
GO
ALTER TABLE [dbo].[NotificationQueue]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[NotificationSetting]  WITH CHECK ADD FOREIGN KEY([notification_type_id])
REFERENCES [dbo].[NotificationType] ([id])
GO
ALTER TABLE [dbo].[NotificationSetting]  WITH CHECK ADD FOREIGN KEY([preference_id])
REFERENCES [dbo].[Preference] ([id])
GO
ALTER TABLE [dbo].[Permission]  WITH CHECK ADD FOREIGN KEY([role_id])
REFERENCES [dbo].[Role] ([id])
GO
ALTER TABLE [dbo].[PollAnswer]  WITH CHECK ADD FOREIGN KEY([created_by])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[PollAnswer]  WITH CHECK ADD FOREIGN KEY([question_id])
REFERENCES [dbo].[PollQuestion] ([id])
GO
ALTER TABLE [dbo].[PollQuestion]  WITH CHECK ADD FOREIGN KEY([channel_id])
REFERENCES [dbo].[Channel] ([id])
GO
ALTER TABLE [dbo].[PollQuestion]  WITH CHECK ADD FOREIGN KEY([created_by])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[PollVotingHistory]  WITH CHECK ADD FOREIGN KEY([answer_id])
REFERENCES [dbo].[PollAnswer] ([id])
GO
ALTER TABLE [dbo].[PollVotingHistory]  WITH CHECK ADD FOREIGN KEY([question_id])
REFERENCES [dbo].[PollQuestion] ([id])
GO
ALTER TABLE [dbo].[PollVotingHistory]  WITH CHECK ADD FOREIGN KEY([voted_by])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[Preference]  WITH CHECK ADD FOREIGN KEY([language_id])
REFERENCES [dbo].[Language] ([id])
GO
ALTER TABLE [dbo].[Preference]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[Workspace]  WITH CHECK ADD FOREIGN KEY([owner_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[WorkspaceMember]  WITH CHECK ADD FOREIGN KEY([role_id])
REFERENCES [dbo].[Role] ([id])
GO
ALTER TABLE [dbo].[WorkspaceMember]  WITH CHECK ADD FOREIGN KEY([user_id])
REFERENCES [dbo].[User] ([id])
GO
ALTER TABLE [dbo].[WorkspaceMember]  WITH CHECK ADD FOREIGN KEY([workspace_id])
REFERENCES [dbo].[Workspace] ([id])
GO
/****** Object:  StoredProcedure [dbo].[get_dms_by_user_id]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[get_dms_by_user_id]
    @user_id INT
AS
BEGIN
    SELECT
        DISTINCT dm.id AS dms_id,
        user1,
        user2
    FROM [Message] m
        JOIN DirectMessage dm ON m.dms_id = dm.id AND dm.user1 = @user_id OR dm.user2 = @user_id
    WHERE sender_id != @user_id;
END

GO
/****** Object:  StoredProcedure [dbo].[proc_get_notification]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[proc_get_notification]
    @notification_type_id INT,
    @user_id INT
AS
BEGIN
    SELECT *
    FROM NotificationQueue
    WHERE 
        user_id = @user_id
        AND is_read = 0
        AND notification_type_id = @notification_type_id
END

GO
/****** Object:  StoredProcedure [dbo].[proc_member_active_time]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[proc_member_active_time]
    @workspace_id INT,
    @is_previous TINYINT
AS
BEGIN
    DECLARE @day INT;

    IF @is_previous = 0
        SET @day = -6;
    ELSE
        SET @day = -12;

    WITH
        days_7
        AS
        (
                            SELECT
                    CASE
                WHEN @is_previous = 1 THEN DATEADD(DAY, -6, GETDATE())
                ELSE GETDATE()
            END AS day
            UNION ALL
                SELECT DATEADD(DAY, -1, day)
                FROM days_7
                WHERE day > DATEADD(DAY, @day, GETDATE())
        ),
        get_workspace
        AS
        (
            SELECT
                ld.event_parameter_id,
                ld.[value],
                l.log_time
            FROM
                [Log] l
                LEFT JOIN [EventType] et ON et.id = l.event_type_id AND et.[event_type_name] = 'User Online'
                LEFT JOIN [EventParameter] ep ON ep.event_type_id = et.id
                LEFT JOIN LogDetail ld ON ld.log_id = l.id AND ld.event_parameter_id = ep.id
        ),
        get_time
        AS
        (
            SELECT

                [value] as time_online,
                log_time
            FROM
                get_workspace
            WHERE event_parameter_id = 2
            GROUP BY 
            event_parameter_id, value, log_time
        )
    SELECT
        day,
        SUM(CONVERT(FLOAT,time_online))/COUNT(*) AS avg_time_online
    FROM
        days_7
        LEFT JOIN get_time ON CAST(log_time AS DATE) = CAST(day AS DATE)
    GROUP BY 
            day
    ORDER BY 
            day DESC

END
GO
/****** Object:  StoredProcedure [dbo].[proc_member_in_workspace]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[proc_member_in_workspace]
    @workspace_id INT
AS
BEGIN
    SELECT
        COUNT(user_id) as new_member
    FROM WorkspaceMember as wm
    WHERE wm.workspace_id = @workspace_id
    GROUP BY wm.workspace_id
END

GO
/****** Object:  StoredProcedure [dbo].[proc_member_left_count]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[proc_member_left_count]
    @workspace_id INT
AS
BEGIN
    SELECT
        COUNT(*) AS member_left_count
    FROM
        WorkspaceMember
    WHERE
        CAST(left_at AS DATE) = CAST(GETDATE() AS DATE)
        AND workspace_id = @workspace_id
END

GO
/****** Object:  StoredProcedure [dbo].[proc_new_member_in_workspace]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[proc_new_member_in_workspace]
    @workspace_id INT
AS
BEGIN
    SELECT
        w.name,
        COUNT(user_id) as new_member
    FROM WorkspaceMember as wm
        JOIN Workspace AS w on w.id = wm.workspace_id
    WHERE CAST(wm.join_at as DATE) = CAST(GETDATE() AS DATE) -- current
        AND w.id = @workspace_id
    GROUP BY w.name
END

GO
/****** Object:  StoredProcedure [dbo].[proc_new_message]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[proc_new_message]
    @user_id INT
AS
BEGIN
    WITH
        id_dms
        AS
        (
            SELECT
                id
            FROM DirectMessage
            WHERE user1 = @user_id OR user2 = @user_id
        )
    SELECT
        COUNT(*) AS new_message
    FROM
        message
    WHERE 
  dms_id IN (SELECT id
        FROM id_dms) AND
        sender_id != @user_id AND
        status_id = 2
END

GO
/****** Object:  StoredProcedure [dbo].[proc_upcoming_event]    Script Date: 18/07/2024 11:03:06 SA ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[proc_upcoming_event]
    @user_id INT
AS
BEGIN
    WITH
        get_meeting_id
        AS
        (
            SELECT *
            FROM MeetingParticipant
            WHERE user_id = @user_id and status_id = 1
        )
    SELECT
        COUNT(id) AS upcoming_event
    FROM Meeting
    WHERE 
        id IN (SELECT meeting_id
        FROM get_meeting_id) AND
        CAST(start_at AS DATE) = CAST(GETDATE() AS DATE)
END

GO
```