# Human Resources | Applications | EN | OFBIz QuickStart
- Managing business employees
- Recruitment process
- Well integrated with other components (especially Accounting for Payroll) and any specific employee [agreements](../agreements/README.md)

## Human Resources Processes
- Job Planning and Definition
    - Generally authorized by: 
        - budget
        - fulfilled by people
    - Fulfilled by: 
        - Permanent employee
        - Temporary employee
        - Contractor
    - Positions: 
        - May be salary or hourly, fulltime or part time
        - Have responsibilies
        - Defined by a type of work
    - Example: 
        - 20 job positions for an administration clerk
        - Each position has a job description
        - They are each authorised by a budget request from a department in the org.
        - A position can be unfulffiled
        - Some other cases: 
            - full-time equivalent (FTE)
            - Can be assigned to more than one person (e.g. job sharing)
    - OFBiz Human Resources application you can: 
        - Create positions
        - Fulfill positions
        - Define the responsibilities of a position
        - Define a tree reporting structure between positions
        - Track the positions fulfillments over time
- Recruitment (Candidate Selection and Hiring)
    - Create a Requisition for new job positions
    - Create Internal Job Postings
    - Apply for job positions
    - Review Resumes / CVs
    - Arrange and Grade Interviews
- Candidate Selection and Hiring
- Employee Training and Development
    - Define and create training courses
    - Schedule courses on a global training calendar
    - Make course available (or unavailable) for enrollment
    - Review and approve requests from employees to attend
- Employee Evaluation and Performance Management
    - Create a new Performance Review for an employee
    - Add individual review items such as Attitude, Communication or Technical Skills
    - Add ratings or comments to each item
- Employee Salary and Benefits
    - Create Pay Grades
    - Link Salary Steps within each Pay Grade
    - Assign a Pay Grade and Salary Step to a Job Position filled by an Employee
    - Manage employee holidays (leave)
    - Manage associated benefits
    - Calculate salaries and Generate Payslips
## Employee Positions
- the work description and responsibilities
- a pay structure (e.g. hourly wages, salary, contract etc)
- full-time or part-time
- the skills needed to fullfill the position

> An employee positions is not the same as a person fullfilling the role. A person fulfilling an employee position is called an employee

> In some cases an employee position could also be considered a full-time equivalent (FTE) and can be assigned to more than one person (e.g. job sharing)

In OFBiz Human Resources application you can: 
- Create employee positions
- Fulfill employee positions
- Define the responsibilities of an employee position
- Define a tree reporting structure between employee positions
- Track employment position fulfillments over time

## Employees
- EIther full time or part-time under formal employment contract
- Paid with wages or salary

> Wages tend to be related to an hourly rate and can vary based on the hours worked whereas salary is a flat rate generally paid monthly.

- Manage info about people
- Manage employement relationship with your company or one its departments
- Employee details: 
    - Profile
    - Display of all employee related information in a single screen
    - Manage employees: 
        - skills
        - qualifications
        - training
        - leave
        - payroll history

You can: 
- Create a new employee
- Search for an existing employee
- View the full list of existing employees

## Employments
- Is a relationship between a person and your Company
- Tracking employment: 
    - benefits
    - pay history
    - unemployment claims
    - employment agreements

> If a person was entered into the application by some other means then you will have to create the employee relationship manually in the Party Manager application.

What is included: 
- start and end date of employment
- type of termination and a reason
- create employment
- find for existing employments

## Performance Review
- post reviews
- management can use reviews
- reports that look at ratings for a review item by position

### Performance Review Item
- rate list of items and commented on
- performance reviews can be created and deleted **but** cannot be changed

You can: 
- Create performance review
- Search performance review
- Update performance review
- Add performance review item
- Delete performance review item

## Qualifications
- Feature of recruitment process
- Verify the minimum set of qualifications as a requirement for a positions
- Capture of the qualification and verification
- Qualifications can be added at any time
- Qualifications can expire of not renewed (expiry and renewal date) (e.g.: Kafka certification with a ~3 year limit for validity)

## Recruitment
- Fulfill roles that you have available
- Job Requisition -> job position that needs to be fulfilled
- Job Requisition identifies: 
    - skills
    - qualifications
    - experience
    - number of resources needed for a position
- Default is Job Requisition is for Internal Job posting
- Requisition needs to be created then create Job Posting based on the requisition
- Example: 
   - The requisition was for 3 roles
   - Then three job postings can be created
   - Each job with a application deadline
- People can apply
- Send their CVs or Resumes
- Track the progress of the application
- Create details about various types of job interviews
    - HR
    - Panel
    - Case Study/Practical Test
    - etc
- Link to the requisition
- Track the status of people that have applied for a position

You can: 
- Approve or reject job applications
- Manage and book job interviews
- Record the result of job interviews

## Skills
- Types: general and specific
- Characterised: years of experience, rating or level of expertise
- OFBiz basic skills can be defined in Global HR Settings
- linked to actual individuals via the Skills menu option
- Skills are part of the *job requisition*
- Record and track their newly acquired skills
    - With this you might find an employee that already has the skills that you are looking for so no need to hire anyone else

You can: 
- Assign or link skills to job applicants (i.e. non employees)
- Assign or link skills to existing employees
- Search for existing employees that have the required skills for a job

## Resumes
- Resumes or Curriculum Vitae (CVs)
- enter a resume as a document and then link it to a person
- resume entry has a unique identifier (that currently needs to be manually entered!)

> The OFBiz Content Manager application is used for the linking of resumes because it was designed for managing, storing and retrieving electronic data in varying formats - such as text, images, MS Word, PDF or even web URL’s.

## Training
- fill any gaps in skills and improve the proficiency of the existing workforce
- HR module includes: 
    - Training Calendar (things that can be scheduled)
        - training classes
        - events
- HR administrator can: 
    - create
    - assign
    - approve training classes
- All other users can: 
    - classes available
    - their training status
    - any requests they have made to enroll for training
- General Process Flow
    - Training classes are created in the Global HR Training Class Type screen
    - Training classes are scheduled and added to the training calendar
    - Employees can create a request to attend a training
    - The employee supervisor needs to approve or reject the employee training request
    - Employees can check the status of the training requests
- Training Calendar
    - This is the main screen
    - From here you add classes and participants
    - You can navigate the calendar by clicking the navigation text for day, week and month views located in the calendar title bar
- Add New Training Event
    - In the Training Calendar you can click on Add New (located in each calendar day cell)
    - This action opens a small window above the calendar to enter the training class details
    > If you try to create a class and do not have correct User permissions, you will get an error. After a class is created a numeric class identifier and text identifier description appear in the calendar for the day of the class.
- Request Training / Add a Training Participant
    - by clicking on the class identifier you can add participants
    - If you are the creator of the class the Participants window above and to the right of the calendar opens
    - 
- Approve Training
    - The training administrator navigates to the Training Approvals screen
    - Locates all requests with a status of "Assigned"
    - 

## Leave

## Security

## Global HR Settings

## Glossary
- **Annual Revenue**
    - Annual revenue is the amount of revenue for a group that is reported in the Party Group Information screenlet of the groups profile (visit Party Profile screen).
- **Budget**
    - A budget is used to track spending in the company for a future period of time. The company may have one or more budgets depending on the requirements i.e. Operating Budget, Capital Budget. A budget has a status, type and is composed of budget line items.
- **Employee**
    - An employee is a person who has an employment relationship with your Company.
- **Employee Position Type**
    - Employee Positions Type is a name that describes a position. Business Analyst, Programmer and System Administrator are examples of position types in the OFBiz demo data. You can define your own position types in Global HR Settings > Position Types.
- **Employment**
    - Employment defines the relationship between your Company and a person who is an employee. The employment relationship tracks employee benefits preferences, pay history, and unemployment claims and agreements.
- **Exempt Flag**
    - The exempt flag can be used to indicate if an employee position is exempt or non-exempt under the fair labor Standards Act (FLSA).
- **Fulfillment**
    - A fulfillment associates a person with a position. A person can fulfill more than one position and a position can have more then one person.
- **Fulltime Flag**
    - The fulltime flag can be used to indicate if an employee position is for a full or part time position.
- **HR App Menu**
    - The main menu that opens the high level features of the HR App i.e. Employees, Employments, Employee Position etc.
- **Internal Organization**
    - Internal organization is the name of a relationship between a party group and your company. This relationship is used to filter party groups as being part of your company to distinguish them from other groups which are external. For example your marketing department is an internal organization while a suppliers sales department is not.
- **Number of Employees**
    - Number of employees that are reported in the Party Group Information screenlet of the groups profile (Visit Party Profile screen).
- **Party**
    - Party is a term used to simplify collecting information that used in a common manner by different people and things. The most common party types are people and groups. Both people and groups have contact information. A party is identified by a unique Party Id. Using this Id OFBiz can collect and find contact (and other information and processes) for both people and groups in the same way. This is why you will often see Party Id as a field in a form or a filter as you work in OFBiz.
- **Party Id**
    - The unique identifier for a party. The **Id is text** so in some cases you will see an Id, created by a user, that carries some meaning i.e. Party Id DemoEmployee. In other cases the Id is created by OFBiz and is will be simply a number from a sequence. In either case the Id is unique.
- **Qualifications**
    - Qualifications for an individual person or organization are in the Employees Qualifications menu item. To find and update the qualifications of people and organizations visit Qualifications menu.
- **Party Qualification Type**
    - Party qualifications define a person or organizations accomplishments that indicate their suitability to perform a job. Qualifications are organized into qualification groups for the purpose of managing and reporting.
- **Person**
    - Person is a human being as distinguished from a **party group which is an organization**. Human beings and organizations have different attributes i.e. People have first and last names while groups have group names. Both person and party group are types of parties and share information and processes common to parties.
- **Position**
    - A position is a job that can be filled by more then one person over time or at the same time. Positions are defined by a type of work. For example there may be 20 positions in an organization for a secretary. Each position is related to a department in the organization. A position can me thought of as a full-time equivalent employee (FTE). So an FTE may be assigned to one or more positions and position can be assigned to more then one FTEs (job sharing).
- **Rating**
    - Rating is a user defined numeric rating for a skill. (See Skills Menu)
- **Responsibility**
    - Responsibilities define duties assigned to a position. They are defined in **Responsibility Types** and assigned in **Employee Position Responsibilities**.
- **Salary Flag**
    - The salary flag can be used to indicate if an employee position is salaried or paid hourly.
- **Skill**
    - Skill is some ability or knowledge possessed by a person or organization that is needed to perform a job for the company. See Skills
- **Skill Level**
    - Skill level is a user defined numeric rating a skill. It is up to the user to assign some meaning to the level. For example 1=Entry, 2=Intermediate, 3=Expert (See Skills Menu).
- **Skill Group**
    - Skill goup is a name that describes a collection of skills that have common attributes (See Skills Menu).
- **Temporary Flag**
    - A temporary flag can be used to indicate if an employee position is permanent or temporary.
- **Termination Reason**
    - The termination reason is a name describing the cause related to a termination type e.g. Type: resigned for reason: found new job.
- **Termination Type**
    - The termination type is a name for the kind of termination e.g. Resigned, fired, retired, layoff.
