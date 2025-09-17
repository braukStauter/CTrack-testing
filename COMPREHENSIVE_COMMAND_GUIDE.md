# CTrack Comprehensive Command Guide

## Overview
This document provides a complete reference of all commands available in CTrack, organized by functional group and permission level.

## Permission Levels
- **Server Owner**: Full access to all commands including initialization
- **Admin**: Administrative privileges (admin_role_ids)
- **Training Admin**: Training management privileges (training_admin_role_ids)
- **Instructor/Mentor**: Training staff privileges (is_instructor/is_mentor flags)
- **Member**: Basic user access (member_role_ids)
- **Developer**: Special development commands (dev_role_ids)

---

## Server Owner Commands

### Server Initialization
**Permission Required**: Server Owner Only

#### `/admin init`
- **Description**: Initialize CTrack for the server
- **Function**: Guides through complete server setup
- **Setup Steps**:
  - ARTCC information configuration
  - Role mapping (Admin, Training Admin, Training Staff, Member)
  - Feature flag configuration
  - Channel and category creation
- **One-time Use**: Should only be run once per server

---

## Administrative Commands (Admin Permissions)

### Core Administration (`/admin`)

#### Server Management
- **`/admin channel-recovery`**
  - **Description**: Verify and recreate missing embeds
  - **Function**: Scans for missing dynamic embeds and recreates them
  - **Use Case**: Fixing corrupted or deleted bot messages

### Student Management (`/admin student`)

#### Status Management
- **`/admin student set-status <student> <status>`**
  - **Description**: Set a student's training or waitlist status
  - **Statuses**: Active, Inactive, Standby, Hold (Academy), Hold (Hours), Hold (Validation), Hold (Admin) Contact TA
  - **Logic**:
    - Active/Inactive: Only for students NOT on waitlist
    - Hold statuses: Only for students ON waitlist
  - **Multi-waitlist**: Prompts for selection if student on multiple waitlists

- **`/admin student inactive <student> [silent]`**
  - **Description**: Set student to inactive and remove from waitlist
  - **Function**: Updates status, removes from waitlist, sends DM (unless silent)
  - **Silent Option**: Skips notification DM

- **`/admin student archive <student> [silent]`**
  - **Description**: Archive student's training record
  - **Function**: Sets status to Archived, removes from waitlist
  - **Use Case**: Student completing training or leaving program

#### Waitlist Management
- **`/admin student add-to-waitlist <user>`**
  - **Description**: Manually add user to waitlist
  - **Function**: Opens modal for training type selection
  - **Options**: Primary, Visitor, Specialized (with type selection)

- **`/admin student set-waitlist-date <user> <date>`**
  - **Description**: Manually set the 'date added' for waitlist entry
  - **Format**: YYYY-MM-DD
  - **Function**: Updates timestamp and reorders waitlist

#### Records & Documentation
- **`/admin student view-inactive-archived`**
  - **Description**: View all students with Inactive or Archived status
  - **Function**: Generates comprehensive list with details

- **`/admin student manage-waitlist-notes <user>`**
  - **Description**: Add, edit, or remove notes for student on waitlist
  - **Multi-waitlist**: Prompts for selection if on multiple waitlists
  - **Function**: Opens modal for note editing

- **`/admin student manage-ots-notes <user>`**
  - **Description**: Manage notes for student on OTS waitlist
  - **Function**: Edit notes for OTS nominations

#### OTS Management
- **`/admin student ots-return <student>`**
  - **Description**: Return OTS-claimed student back to OTS waitlist
  - **Function**: Cancels active OTS, returns to waitlist

- **`/admin student ots-cancel <student>`**
  - **Description**: Cancel student's OTS nomination entirely
  - **Function**: Removes from OTS, returns to original instructor

### Assignment Management (`/admin`)

#### Assignment Operations
- **`/admin assign-student <student> <instructor> [waitlist_type]`**
  - **Description**: Assign student from waitlist to instructor
  - **Waitlist Types**: Primary, Specialized
  - **Auto-detection**: Prompts for type if student on multiple waitlists
  - **Function**: Creates assignment, sends notification, removes from waitlist

- **`/admin remove-student <student>`**
  - **Description**: Remove student's assignment
  - **Function**: Cancels assignment, restores to original waitlist
  - **Channel Access**: Removes student from instructor channel

### Instructor Management (`/admin`)

#### Capacity Management
- **`/admin set-max-students <user> <max_students>`**
  - **Description**: Set maximum student load for instructor/mentor
  - **Range**: 1-10 students
  - **Validation**: User must be instructor or mentor
  - **Function**: Updates capacity, reflects in dashboards

### Training System Configuration

#### Specialized Training (`/admin training-types`)
- **`/admin training-types add`**
  - **Description**: Add new specialized training type
  - **Function**: Opens modal for training type name entry

- **`/admin training-types list`**
  - **Description**: List all specialized training types
  - **Function**: Shows type IDs and names

- **`/admin training-types remove`**
  - **Description**: Remove specialized training type
  - **Function**: Selection menu for type removal

#### Form Management (`/admin form`)
- **`/admin form create <form_type>`**
  - **Description**: Create new form for students or instructors
  - **Form Types**: Student, Instructor
  - **Function**: Opens modal for form configuration with JSON questions

- **`/admin form remove`**
  - **Description**: Remove custom form
  - **Function**: Selection menu for form removal

#### Progress Requirements (`/admin config`)
- **`/admin config set-progress-requirements`**
  - **Description**: Set up progress requirements for ratings
  - **Interactive**: Guided setup for S1, S2, S3, C1 ratings
  - **Configuration**: Training hours, positions, OTS hours, OTS positions

- **`/admin config view-progress-requirements`**
  - **Description**: View existing progress requirements
  - **Function**: Shows all configured rating requirements

### Team Communication (`/admin notice`)

#### Notice Management
- **`/admin notice new`**
  - **Description**: Post new notice to team notice board
  - **Function**: Modal for content and expiration
  - **Expiration**: Optional expiration in days

- **`/admin notice manage <notice_id>`**
  - **Description**: Manage existing team notice
  - **Functions**: View, edit, change expiration, delete

### Comprehensive Reporting (`/admin reports`)

#### Report Overview
- **`/admin reports help`**
  - **Description**: View all available reports and descriptions
  - **Function**: Comprehensive documentation of reporting system

#### User Reports
- **`/admin reports user <user>`**
  - **Description**: Generate comprehensive report for specific user
  - **Input**: Discord mention, Discord ID, or VATSIM CID
  - **Content**: Waitlist positions, training stats, assignment history

- **`/admin reports req <request_id>`**
  - **Description**: View details for specific form submission
  - **Function**: Shows submission details with action buttons

- **`/admin reports req-all [user]`**
  - **Description**: View all form submissions
  - **Filter**: Optional user filter
  - **Time Range**: Last 90 days by default

#### Training Reports
- **`/admin reports obs`**
  - **Description**: Generate report of all OBS students
  - **Function**: Lists inactive students with export file

- **`/admin reports ins`**
  - **Description**: Comprehensive instructor performance report
  - **Content**: Student loads, capacity utilization, activity metrics
  - **Export**: Text file with detailed statistics

- **`/admin reports waitlist [rating]`**
  - **Description**: Current waitlist status report
  - **Filter**: Optional rating filter
  - **Export**: Detailed waitlist analysis with text file

- **`/admin reports group-sessions [days]`**
  - **Description**: Group session statistics
  - **Time Range**: 1-365 days (default 30)
  - **Content**: Attendance metrics, popular sessions

- **`/admin reports progress <user> <rating>`**
  - **Description**: View progress report for user towards rating
  - **Function**: VATSIM hours analysis against requirements
  - **Input**: User identifier and target rating

### System Configuration (`/admin config`)

#### Embed Management
- **`/admin config refresh-embeds`**
  - **Description**: Refresh all embeds in the server
  - **Function**: Updates all dynamic embeds with current data

#### Message Configuration
- **`/admin config set-message <message_name>`**
  - **Description**: Set configurable message for the bot
  - **Message Types**: inactive_dm, archive_dm, training_policy
  - **Function**: Custom message content for automated notifications

---

## Instructor/Mentor Commands (Training Staff Permissions)

### Session Management (`/ins sessions`)

#### Session Creation
- **`/ins sessions post-impromptu`**
  - **Description**: Post new impromptu training session
  - **Requirements**: Timezone configured
  - **Function**: Modal for session details, conflict checking
  - **Parameters**: Start/end time, rating restrictions

- **`/ins sessions new-fixed`**
  - **Description**: Post new fixed-time training session
  - **Requirements**: Timezone configured, 1+ hour in future
  - **Function**: Scheduled session creation
  - **Parameters**: Start time, duration, restrictions

- **`/ins sessions new-block`**
  - **Description**: Post new availability block
  - **Requirements**: Timezone configured
  - **Function**: General availability posting
  - **Parameters**: Date, start/end time

#### Session Administration
- **`/ins sessions manage`**
  - **Description**: Modify or cancel upcoming sessions
  - **Scope**: Open impromptu, unclaimed fixed, claimed sessions
  - **Actions**: Cancel, modify, update restrictions

- **`/ins sessions manage-availability`**
  - **Description**: Modify or delete availability blocks
  - **Scope**: Open availability blocks only
  - **Actions**: Modify times, delete blocks

- **`/ins sessions closeout`**
  - **Description**: Closeout past training sessions
  - **Scope**: Past claimed sessions requiring closeout
  - **Statuses**: Completed, No-show, Cancelled, Incomplete

#### Group Sessions
- **`/ins sessions post-group`**
  - **Description**: Post new group training session
  - **Requirements**: Timezone configured
  - **Function**: Group session with signup functionality
  - **Parameters**: Name, description, times, max seats

- **`/ins sessions manage-group`**
  - **Description**: Manage posted group sessions
  - **Scope**: Upcoming group sessions
  - **Functions**: View attendees, modify details, mark attendance

### Student Interaction (`/ins student`)

#### Assignment Management
- **`/ins student assign-special <list_number>`**
  - **Description**: Claim student from specialized/visitor waitlist
  - **Function**: Assignment by waitlist position number
  - **Process**: Creates assignment, sends notification

#### Student Records
- **`/ins student records <user>`**
  - **Description**: View student's training records
  - **Sources**: Local sessions and VATUSA records
  - **Input**: Discord mention, VATSIM CID, Discord ID, or name
  - **Function**: Comprehensive training history view

### OTS Operations (`/ins ots`)

#### OTS Evaluation
- **`/ins ots pass <student>`**
  - **Description**: Pass student's OTS
  - **Function**: Completes OTS, returns to primary waitlist with Hold (Hours)
  - **Access**: Removes from instructor channel

- **`/ins ots fail <student>`**
  - **Description**: Fail student's OTS
  - **Function**: Returns student to original instructor
  - **Process**: Creates new pending assignment requiring acceptance

---

## Student Commands (Member Permissions)

### Student Information (`/student`)

#### Assignment Status
- **`/student my-instructor`**
  - **Description**: Shows assigned instructor
  - **Unassigned**: Directs to waitlist in training channel
  - **Assigned**: Shows instructor details and channel access

#### Training Resources
- **`/student help`**
  - **Description**: Get help with training process
  - **Function**: Links to policy and forms channels
  - **Purpose**: Direct students to resources and request forms

#### Progress Tracking
- **`/student progress <rating>`**
  - **Description**: View progress towards rating requirement
  - **Requirements**: Linked VATSIM account, configured requirements
  - **Function**: VATSIM hours analysis against rating requirements
  - **Ratings**: S1, S2, S3, C1 (based on configuration)

---

## Personal Settings (All Users)

### User Configuration (`/set`)

#### Timezone Management
- **`/set timezone`**
  - **Description**: Set local timezone for time displays
  - **Options**: US timezones (Eastern, Central, Mountain, Pacific, Alaska, Hawaii)
  - **Function**: Affects all time displays throughout system
  - **Requirement**: Must be set before using session commands

---

## Developer Commands (Developer Permissions)

### Development Tools (`/dev`)

#### API Configuration
- **`/dev vatusa-on`**
  - **Description**: Switch to live VATUSA API
  - **Function**: Changes API mode to production

- **`/dev vatusa-off`**
  - **Description**: Switch to local mock VATUSA data
  - **Function**: Changes API mode to development/testing

#### Testing Tools
- **`/dev fast-mode <enabled>`**
  - **Description**: Toggle faster background task evaluation
  - **Function**: Changes sync interval from 15 minutes to 1 minute
  - **Purpose**: Testing and development acceleration

#### Profile Management
- **`/dev set-profile [rating] [is_instructor] [is_mentor]`**
  - **Description**: Temporarily modify user profile for testing
  - **Function**: Override profile data until next roster sync
  - **Use Case**: Testing features requiring specific roles/ratings

- **`/dev inject-user <user> <vatsim_cid> <first_name> <last_name> <rating> <facility> [is_instructor] [is_mentor]`**
  - **Description**: Inject test user into database
  - **Function**: Create/update user with specified details
  - **Purpose**: Testing with controlled user data

---

## Interactive Elements (No Commands)

### Embed Interactions

#### Training Channel
- **Waitlist Embed**: Join/leave waitlist buttons
- **Session Embeds**: Claim impromptu sessions, sign up for group sessions
- **Assignment Embed**: View current assignments

#### Forms Channel
- **Student Forms**: Access student form submissions
- **Instructor Forms**: Access instructor form submissions (instructor+ only)

#### Admin Channel
- **Training Activity**: Monitor recent training activity
- **Support Requests**: View and manage form submissions
- **OTS Waitlist**: Monitor OTS nominations and claims

#### Team Channel
- **Notice Board**: View team notices and mark as reviewed
- **Instructor Dashboards**: Individual instructor session management

---

## Permission Matrix

| Command Group | Server Owner | Admin | Training Admin | Instructor | Member |
|---------------|--------------|-------|----------------|------------|--------|
| `/admin init` | ✅ | ❌ | ❌ | ❌ | ❌ |
| `/admin` (general) | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/admin student` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/admin assign-student` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/admin remove-student` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/admin set-max-students` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/admin training-types` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/admin form` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/admin notice` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/admin reports` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/admin config` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `/ins sessions` | ✅ | ✅ | ✅ | ✅ | ❌ |
| `/ins student` | ✅ | ✅ | ✅ | ✅ | ❌ |
| `/ins ots` | ✅ | ✅ | ✅ | ✅ | ❌ |
| `/student` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `/set` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `/dev` | ✅ | ❌ | ❌ | ❌ | ❌* |

*Developer role required for `/dev` commands regardless of other permissions

---

## Command Dependencies & Prerequisites

### Timezone Requirement
**Required for these commands**:
- All `/ins sessions` commands
- Session time displays
- Report time formatting

**Set via**: `/set timezone`

### Database Requirements
**User must exist in database for**:
- Assignment operations
- Student management
- Progress tracking
- Training records

**Populated via**: VATUSA roster sync or manual injection

### VATSIM Integration
**Required for**:
- `/student progress` - needs linked VATSIM CID
- `/admin reports progress` - needs target user's VATSIM CID
- Training records lookup

### Configuration Dependencies
- **Progress requirements**: Must be configured for progress commands
- **Specialized training**: Must be enabled for specialized waitlist functions
- **Role mapping**: Required for permission checking
- **Channel configuration**: Required for embed interactions

---

## Error Handling

### Common Error Scenarios
1. **Permission Denied**: User lacks required role/permission
2. **Missing Configuration**: Required settings not configured
3. **Invalid User**: User not found or not in database
4. **Timezone Required**: Timezone not set for time-dependent commands
5. **Conflict Detection**: Session scheduling conflicts
6. **Data Validation**: Invalid parameters or formats

### Graceful Degradation
- Commands fail safely with informative error messages
- Partial functionality when some features unavailable
- Fallback to alternative methods when primary systems fail

---

This comprehensive guide covers all available commands in CTrack organized by permission level and functional group. Each command includes its description, requirements, and key functionality to support thorough testing and proper usage.