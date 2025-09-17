# CTrack Beta Testing Guide - Member Permissions

## Overview
This guide covers functionality available to regular **Members** in CTrack. Members can interact with the training system as students, submit forms, view their progress, and participate in group sessions.

## Prerequisites
- **Role Required**: Member role configured in the guild settings (basic user access)
- **Permissions**: Standard member privileges
- **Access Level**: Student-focused functionality, form submission, progress tracking

---

## Phase 1: Initial Setup & Personal Configuration

### 1.1 Timezone Configuration
**Command**: `/set timezone`
**Steps**:
1. Set personal timezone using dropdown menu:
   - Test all available US timezones (Eastern, Central, Mountain, Pacific, Alaska, Hawaii)
2. Verify timezone affects time displays in subsequent interactions
3. Confirm setting persists between sessions
4. Test changing timezone and verify updates

**Expected Result**: All times display in your selected timezone throughout the system.

---

## Phase 2: Student Functionality & Progress Tracking

### 2.1 Assignment Information
**Command**: `/student my-instructor`
**Steps**:

#### When NOT Assigned:
1. Run command when not assigned to an instructor
2. Verify directed to check waitlist in training channel
3. Confirm proper channel links provided

#### When Assigned:
1. Run command after being assigned to an instructor
2. Verify instructor information displayed
3. Check instructor channel access mentioned
4. Test link to instructor channel

### 2.2 Training Help & Resources
**Command**: `/student help`
**Steps**:
1. Access training help information
2. Verify links to policy channel provided
3. Check forms channel reference for additional help
4. Test channel links for accessibility

### 2.3 Progress Tracking
**Command**: `/student progress <rating>`
**Prerequisites**: Linked VATSIM account, configured progress requirements
**Steps**:

#### Progress Report Testing:
1. Test progress reports for various ratings:
   - `/student progress S1`
   - `/student progress S2`
   - `/student progress S3`
   - `/student progress C1`
2. Verify VATSIM hours data retrieval
3. Check requirement comparisons (training vs OTS requirements)
4. Test with ratings that have no configured requirements (should error gracefully)

#### Data Validation:
1. Test command without VATSIM CID linked (should error)
2. Verify hours data caching functionality
3. Check progress calculations against requirements
4. Test date range information display

---

## Phase 3: Form Submission System

### 3.1 Student Form Submissions
**Location**: Forms channel (via embedded buttons)
**Prerequisites**: Student forms configured by administrators
**Steps**:

#### Form Access:
1. Navigate to forms channel
2. Locate student forms section in embed
3. Click on available student forms
4. Verify form modal opens properly

#### Form Completion:
1. Complete various types of student forms:
   - Required field validation
   - Optional field handling
   - Text length limits
2. Submit forms with different data types
3. Test form submission confirmation

#### Form Management:
1. Submit multiple forms to test system capacity
2. Test rapid successive submissions
3. Verify submission tracking and status

### 3.2 Form Interaction Validation
**Steps**:
1. Attempt to access instructor forms (should be restricted or error)
2. Test form submission without required fields (should error)
3. Verify proper error messages for invalid submissions

---

## Phase 4: Waitlist & Assignment Interaction

### 4.1 Waitlist Self-Service
**Location**: Training channel waitlist embed
**Prerequisites**: Configured for waitlist participation
**Steps**:

#### Waitlist Interaction:
1. Use waitlist embed buttons to join primary waitlist
2. Test specialized waitlist joining (if available)
3. Verify waitlist position updates correctly
4. Test leaving waitlist functionality

#### Status Monitoring:
1. Monitor waitlist position changes
2. Verify status updates (Standby, Hold statuses, etc.)
3. Check waitlist notes display (if any)

### 4.2 Assignment Acceptance
**Prerequisites**: Assignment notification received from instructor/admin
**Steps**:

#### Assignment Notification:
1. Receive assignment notification via DM
2. Review assignment details (instructor, training type)
3. Test assignment acceptance button
4. Test assignment decline button

#### Post-Assignment:
1. Verify access to instructor channel after acceptance
2. Confirm waitlist removal after acceptance
3. Test instructor communication capabilities
4. Verify assignment appears in assignments embed

---

## Phase 5: Training Session Participation

### 5.1 Impromptu Session Interaction
**Location**: Training channel
**Prerequisites**: Posted impromptu sessions by instructors
**Steps**:

#### Session Claims:
1. Claim available impromptu sessions matching your rating
2. Test claiming sessions with rating restrictions
3. Attempt to claim restricted sessions (should error appropriately)
4. Verify session status updates after claiming

#### Session Communication:
1. Communicate with instructor after claiming session
2. Test session cancellation (if needed)
3. Verify proper notifications throughout process

### 5.2 Group Session Participation
**Location**: Training channel
**Prerequisites**: Posted group sessions by instructors
**Steps**:

#### Session Signup:
1. Sign up for available group sessions
2. Test maximum capacity limits (join sessions near capacity)
3. Attempt to join full sessions (should error gracefully)
4. Verify signup confirmation and attendee list updates

#### Session Management:
1. Leave signed-up sessions (test cancellation)
2. Verify reminder notifications (if configured)
3. Test attendance marking (post-session)

---

## Phase 6: OTS (Over-the-Shoulder) Workflow

### 6.1 OTS Nomination Process
**Prerequisites**: Instructor nomination to OTS waitlist
**Steps**:

#### OTS Waitlist:
1. Verify appearance on OTS waitlist after nomination
2. Check OTS waitlist embed display
3. Monitor OTS claim status updates

#### OTS Evaluation:
1. Participate in OTS evaluation when claimed
2. Test communication during OTS process
3. Verify post-OTS status updates (pass/fail scenarios)

---

## Phase 7: Channel Access & Communication

### 7.1 Channel Navigation
**Steps**:

#### Accessible Channels:
1. Test access to training channel (viewing waitlists, sessions)
2. Access forms channel for form submissions
3. View policy channel for training information
4. Access instructor channel when assigned

#### Restricted Access:
1. Verify no access to admin channels
2. Confirm no access to team/staff channels
3. Test proper error handling for restricted areas

### 7.2 Communication Testing
**Steps**:
1. Test DM communication with instructors
2. Verify assignment notification system
3. Test session-related communications
4. Check automated system notifications

---

## Phase 8: Interactive Embed Testing

### 8.1 Training Channel Embeds
**Location**: Training channel
**Steps**:

#### Waitlist Embed:
1. Interact with waitlist buttons (join/leave)
2. Verify position updates and status changes
3. Test specialized waitlist interactions

#### Session Embeds:
1. Claim impromptu sessions
2. Sign up for group sessions
3. Test session interaction buttons
4. Verify proper error handling

### 8.2 Forms Channel Embeds
**Location**: Forms channel
**Steps**:
1. Access student forms via embed buttons
2. Verify instructor forms are restricted
3. Test form submission workflow
4. Check submission status tracking

---

## Phase 9: Error Handling & Permission Boundaries

### 9.1 Permission Testing
**Steps**:
1. Attempt administrative commands (should error)
2. Try instructor-specific commands (should error)
3. Test access to restricted form types
4. Verify proper error messages for unauthorized actions

### 9.2 Data Validation
**Steps**:
1. Test commands with invalid parameters
2. Attempt operations outside your scope
3. Test form submission with invalid data
4. Verify graceful error handling throughout

### 9.3 Edge Case Scenarios
**Steps**:
1. Test rapid button clicking on embeds
2. Attempt multiple simultaneous form submissions
3. Test session claims during high activity
4. Verify system stability under normal use

---

## Expected Behaviors & Validation Points

### Success Indicators:
- Student commands execute without errors
- Form submissions complete successfully
- Waitlist interactions work smoothly
- Assignment acceptance process functions
- Session participation operates correctly
- Progress tracking provides accurate data
- Channel access respects permission boundaries

### Key Validations:
- ✅ Student-focused functionality accessible
- ✅ Progress tracking shows accurate VATSIM data
- ✅ Form submission system works end-to-end
- ✅ Waitlist participation functions correctly
- ✅ Assignment workflow completes properly
- ✅ Session interaction works smoothly
- ✅ Permission boundaries properly enforced
- ✅ Communication systems operational

### Critical Issues to Report:
- Command failures or errors
- Form submission failures
- Waitlist interaction problems
- Assignment process breakdowns
- Session participation issues
- Progress tracking inaccuracies
- Unauthorized access to restricted features
- Communication system failures

---

## Scope Limitations

**Members should NOT have access to**:
- Administrative commands (`/admin` group)
- Instructor commands (`/ins` group)
- Server configuration functions
- Student management operations
- Form management (creation/deletion)
- Advanced reporting functions

**Members SHOULD have access to**:
- Student commands (`/student` group)
- Personal settings (`/set` group)
- Form submission capabilities
- Waitlist interaction
- Session participation
- Progress tracking
- Basic training information

---

## Real-World Usage Scenarios

### 1. New Student Journey
**Complete Workflow**:
1. Set timezone for proper time display
2. Join primary waitlist via embed
3. Submit initial student form with training goals
4. Accept assignment when notified
5. Claim impromptu session from instructor
6. Participate in group sessions
7. Track progress toward rating goals

### 2. Active Training Participation
**Ongoing Activities**:
1. Monitor waitlist position and status
2. Participate in available training sessions
3. Submit forms for specific training requests
4. Communicate with assigned instructor
5. Sign up for relevant group sessions
6. Track hours progress regularly

### 3. OTS Preparation
**Advanced Student Activities**:
1. Monitor progress requirements
2. Work with instructor toward OTS nomination
3. Participate in OTS waitlist when nominated
4. Complete OTS evaluation process
5. Handle post-OTS status changes

---

## Post-Testing Checklist

After completing all tests:
- [ ] Student commands work correctly
- [ ] Progress tracking accurate and informative
- [ ] Form submission system functional
- [ ] Waitlist interactions smooth
- [ ] Assignment process complete
- [ ] Session participation works
- [ ] Channel access appropriate
- [ ] Permission boundaries enforced
- [ ] Communication systems operational
- [ ] Error handling graceful
- [ ] Timezone settings effective
- [ ] Interactive embeds functional
- [ ] Real-time updates working