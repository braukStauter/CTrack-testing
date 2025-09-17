# CTrack Beta Testing Guide - Instructor Permissions

## Overview
This guide covers functionality available to users with **Instructor/Mentor permissions** in CTrack. Instructors can manage their training sessions, student interactions, and participate in the OTS system.

## Prerequisites
- **Role Required**: Instructor or Mentor role (is_instructor or is_mentor flag in database)
- **Permissions**: Training staff privileges
- **Access Level**: Session management, student interaction, specialized assignments

---

## Phase 1: Initial Setup & Timezone Configuration

### 1.1 Personal Settings
**Command**: `/set timezone`
**Steps**:
1. Set your timezone using the dropdown menu:
   - Test various US timezones (Eastern, Central, Mountain, Pacific, Alaska, Hawaii)
2. Verify timezone setting affects all subsequent time displays
3. Confirm setting persists across sessions

**Note**: Timezone must be set before using most session commands.

---

## Phase 2: Session Management & Availability

### 2.1 Impromptu Session Management
**Command**: `/ins sessions post-impromptu`
**Prerequisites**: Timezone configured
**Steps**:

#### Session Creation:
1. Create impromptu sessions with various parameters:
   - Different start/end times (test same day and cross-day)
   - Various restrictions: "All", "S1", "S2", "S3", "C1"
   - Test overlap detection with existing sessions
2. Verify session appears in training channel with proper embed
3. Confirm session ID displayed in embed footer
4. Test interaction buttons (claim/cancel functionality)

#### Edge Case Testing:
1. Attempt to create overlapping sessions (should error)
2. Test invalid time formats
3. Test end time before start time (should error)

### 2.2 Fixed Session Scheduling
**Command**: `/ins sessions new-fixed`
**Prerequisites**: Timezone configured
**Steps**:

#### Session Creation:
1. Schedule fixed sessions at least 1 hour in future:
   - Test various durations (0.5, 1, 2, 3+ hours)
   - Set different rating restrictions
   - Verify future time requirement (should error if too soon)
2. Confirm session appears in instructor dashboard
3. Test overlap detection with existing commitments

#### Validation Testing:
1. Attempt scheduling session less than 1 hour in future (should error)
2. Test invalid duration formats
3. Test scheduling conflicts with existing sessions

### 2.3 Availability Block Management
**Command**: `/ins sessions new-block`
**Prerequisites**: Timezone configured
**Steps**:

#### Block Creation:
1. Create availability blocks:
   - Same-day blocks (start < end time)
   - Overnight blocks (end time next day)
   - Various date formats (YYYY-MM-DD, HH:MM)
2. Verify blocks appear in instructor dashboard
3. Test overlap detection with other commitments

#### Block Management:
1. Use `/ins sessions manage-availability`:
   - View all open availability blocks
   - Modify existing blocks
   - Delete blocks
2. Verify dashboard updates after changes

### 2.4 Session Management
**Command**: `/ins sessions manage`
**Prerequisites**: Existing sessions (Fixed, Impromptu, or claimed)
**Steps**:

#### Session Overview:
1. View all manageable sessions:
   - Open Impromptu sessions
   - Unclaimed Fixed sessions
   - Claimed sessions with students
2. Verify proper session type indicators (🚀 Impromptu, 📅 Fixed, 👥 Group)

#### Session Actions:
1. For each session type, test available actions:
   - Cancel sessions
   - Modify session times
   - Update restrictions/details
2. Verify proper notifications sent to affected students

### 2.5 Session Closeout
**Command**: `/ins sessions closeout`
**Prerequisites**: Past claimed sessions requiring closeout
**Steps**:

#### Closeout Process:
1. Select sessions for closeout from past claimed sessions
2. Test different closeout statuses:
   - "Completed Successfully"
   - "Student No-Show"
   - "Instructor Cancelled"
   - "Incomplete/Rescheduled"
3. Verify session status updates in database
4. Confirm instructor dashboard reflects completed sessions

---

## Phase 3: Group Session Management

### 3.1 Group Session Creation
**Command**: `/ins sessions post-group`
**Prerequisites**: Timezone configured
**Steps**:

#### Session Setup:
1. Create group sessions with various parameters:
   - Different session names and descriptions
   - Various start/end times
   - Different maximum seat limits (test with and without limits)
2. Verify session appears in training channel with signup functionality
3. Test interaction buttons for student signups

#### Session Validation:
1. Test invalid time ranges (end before start)
2. Verify future scheduling requirements
3. Test maximum seat functionality

### 3.2 Group Session Management
**Command**: `/ins sessions manage-group`
**Prerequisites**: Posted group sessions
**Steps**:

#### Session Administration:
1. Select from upcoming group sessions
2. Test management actions:
   - View current attendee list
   - Modify session details
   - Cancel sessions
   - Mark attendance (after session completion)
3. Verify proper notifications to signed-up students

#### Attendance Management:
1. Mark students as "Attended", "Absent", or maintain "Signed Up" status
2. Verify attendance statistics update correctly
3. Test reminder system functionality

---

## Phase 4: Student Interaction & Assignment

### 4.1 Specialized Assignment Claims
**Command**: `/ins student assign-special`
**Prerequisites**: Students on specialized/visitor waitlist
**Steps**:

#### Assignment Process:
1. Claim students from specialized waitlist by list number
2. Verify assignment notification sent to student
3. Confirm student removed from waitlist
4. Check assignment appears in assignments embed
5. Test assignment of already-assigned student (should error)

#### Assignment Types:
1. Test with different specialized training types
2. Test with visitor students (different workflow)
3. Verify proper training type notification in DMs

### 4.2 Student Records Access
**Command**: `/ins student records`
**Prerequisites**: Students in system, VATUSA API access
**Steps**:

#### Record Lookup:
1. Look up student records using various identifiers:
   - Discord mentions (@student)
   - VATSIM CIDs (numerical)
   - Discord IDs
   - Student names
2. Verify both local and VATUSA records display
3. Test with students not in local database (VATUSA-only lookup)

#### Record Review:
1. Review local session history
2. Access VATUSA training records
3. Verify comprehensive training timeline
4. Test with students who have no training history

---

## Phase 5: OTS (Over-the-Shoulder) Operations

### 5.1 OTS Evaluation Management
**Commands**: `/ins ots pass`, `/ins ots fail`
**Prerequisites**: Claimed OTS sessions with students
**Steps**:

#### OTS Pass Process:
1. Pass student's OTS evaluation
2. Verify student status updated to 'Hold (Hours)'
3. Confirm student returned to primary waitlist
4. Check student removed from instructor channel access
5. Verify congratulatory notification sent to student

#### OTS Fail Process:
1. Fail student's OTS evaluation
2. Verify student returned to original instructor with pending assignment
3. Confirm proper notifications sent to all parties
4. Check student removed from OTS instructor channel access
5. Verify assignment notification requires student acceptance

#### OTS Validation:
1. Attempt OTS actions on non-OTS students (should error)
2. Test OTS actions on students assigned to other instructors (should error)
3. Verify proper permission checks

---

## Phase 6: Communication & Channel Access

### 6.1 Instructor Channel Management
**Prerequisites**: Students assigned and accepted
**Steps**:

#### Channel Access:
1. Verify assigned students have access to your instructor channel
2. Test communication within instructor channels
3. Confirm students lose access when assignments end

#### Channel Naming:
1. Verify instructor channel follows naming convention
2. Test with various instructor name formats
3. Confirm channel creation for new instructors

---

## Phase 7: Dashboard & Embed Interaction

### 7.1 Instructor Dashboard
**Prerequisites**: Various session types and assignments
**Steps**:

#### Dashboard Review:
1. View instructor dashboard in team channel
2. Verify all session types display correctly:
   - Open availability blocks
   - Fixed sessions
   - Claimed sessions with student details
   - Group sessions with attendee counts
3. Confirm real-time updates after session modifications

#### Capacity Management:
1. Verify current student load displayed
2. Check maximum capacity indication
3. Test capacity restrictions (if at maximum)

---

## Phase 8: Error Handling & Edge Cases

### 8.1 Permission Validation
**Steps**:
1. Verify instructor commands require proper role
2. Test commands without instructor/mentor role (should error)
3. Confirm graceful error handling for permission failures

### 8.2 Timezone Dependencies
**Steps**:
1. Attempt session commands without timezone set (should prompt)
2. Test timezone setting workflow
3. Verify time display consistency across commands

### 8.3 Conflict Detection
**Steps**:
1. Create overlapping sessions (should error)
2. Test scheduling during existing commitments
3. Verify proper conflict detection across session types

### 8.4 Data Validation
**Steps**:
1. Test with invalid student identifiers
2. Attempt operations on non-existent sessions
3. Verify proper error messages for all failure scenarios

---

## Expected Behaviors & Validation Points

### Success Indicators:
- All instructor commands execute without errors
- Session creation and management works smoothly
- Student assignment and OTS processes function correctly
- Proper time zone handling throughout
- Dashboard updates reflect current status
- Channel access management works properly

### Key Validations:
- ✅ Session scheduling prevents conflicts
- ✅ Group sessions handle signups properly
- ✅ Student assignment notifications work
- ✅ OTS workflow completes correctly
- ✅ Student records accessible and comprehensive
- ✅ Instructor dashboard shows current status
- ✅ Channel access managed automatically

### Critical Issues to Report:
- Session creation failures
- Missing or incorrect time zone handling
- Assignment notification failures
- OTS process errors
- Student record lookup failures
- Dashboard display issues
- Channel access problems
- Permission bypass opportunities

---

## Scope Limitations

**Instructors should NOT have access to**:
- Administrative commands (`/admin` group)
- Server configuration changes
- Student status modifications (except through assignment/OTS)
- Waitlist management commands
- User profile modifications

**Instructors SHOULD have access to**:
- All session management commands
- Student record viewing
- Specialized assignment claiming
- OTS evaluation commands
- Group session management
- Personal timezone settings

---

## Post-Testing Checklist

After completing all tests:
- [ ] All session types create successfully
- [ ] Session management works correctly
- [ ] Group sessions function properly
- [ ] Student assignment process operational
- [ ] OTS evaluation workflow complete
- [ ] Student records accessible
- [ ] Instructor dashboard accurate
- [ ] Channel access management functional
- [ ] Timezone handling consistent
- [ ] Error handling appropriate
- [ ] Permission boundaries respected
- [ ] Real-time updates functioning across embeds