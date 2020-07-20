# Data Models

### DataType Attribute

##### By using data annotation attributes, you can make one code change that will fix the display format in every view that shows the data.

##### Example:

using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;

namespace ContosoUniversity.Models
{
    public class Student
    {
        public int ID { get; set; }
        public string LastName { get; set; }
        public string FirstMidName { get; set; }
        [DataType(DataType.Date)]
        [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
        public DateTime EnrollmentDate { get; set; }

        public ICollection<Enrollment> Enrollments { get; set; }
    }
}

##### DataType attribute is used to specify a data type that's more specific than the database intrinsic type.

##### DataType Enumeration provides for many data types, such as Date, Time, PhoneNumber, Currency, and EmailAddress.

##### The DisplayFormat attribute is used to explicitly specify the date format:

[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]

##### You can use the DisplayFormat attribute by itself, but it's generally a good idea to use the DataType attribute also.

##### The StringLength attribute sets the maximum length in the database and provides client side and server side validation for ASP.NET Core MVC.

##### Example:

using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;

namespace ContosoUniversity.Models
{
    public class Student
    {
        public int ID { get; set; }
        [StringLength(50)]
        public string LastName { get; set; }
        [StringLen get; set; }
        [DataType(DataType.Date)]
        [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
        public DateTime EnrollmentDate { get; set; }

        public ICollection<Enrollment> Enrollments { get; set; }
    }
}

##### The StringLength attribute won't prevent a user from entering white space for a name. Use Regex to fix:

[RegularExpression(@"^[A-Z]+[a-zA-Z]*$")]

##### The Column Attribute specifies that when the database is created, the column of the Student table that maps to the FirstMidName property will be named FirstName. 

##### Example:

using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;

namespace ContosoUniversity.Models
{
    public class Student
    {
        public int ID { get; set; }
        [StringLength(50)]
        public string LastName { get; set; }
        [StringLength(50)]
        [Column("FirstName")]
        public string FirstMidName { get; set; }
        [DataType(DataType.Date)]
        [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
        public DateTime EnrollmentDate { get; set; }

        public ICollection<Enrollment> Enrollments { get; set; }
    }
}

### Create Instructor Entity

##### Example code:

using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;

namespace ContosoUniversity.Models
{
    public class Instructor
    {
        public int ID { get; set; }

        [Required]
        [Display(Name = "Last Name")]
        [StringLength(50)]
        public string LastName { get; set; }

        [Required]
        [Column("FirstName")]
        [Display(Name = "First Name")]
        [StringLength(50)]
        public string FirstMidName { get; set; }

        [DataType(DataType.Date)]
        [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
        [Display(Name = "Hire Date")]
        public DateTime HireDate { get; set; }

        [Display(Name = "Full Name")]
        public string FullName
        {
            get { return LastName + ", " + FirstMidName; }
        }

        public ICollection<CourseAssignment> CourseAssignments { get; set; }
        public OfficeAssignment OfficeAssignment { get; set; }
    }
}

##### The CourseAssignments and OfficeAssignment properties are navigation properties.

public ICollection<CourseAssignment> CourseAssignments { get; set; }
    
### Create OfficeAssignment entity

using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;

namespace ContosoUniversity.Models
{
    public class OfficeAssignment
    {
        [Key]
        public int InstructorID { get; set; }
        [StringLength(50)]
        [Display(Name = "Office Location")]
        public string Location { get; set; }

        public Instructor Instructor { get; set; }
    }
}

### DBMS

##### Database: a collection of related data
##### Data: a collection of facts and figures that can be processed to produce information.
##### Database Management System: stores data in such a way that it becomes easier to retrieve, manipulate, and produce information.

##### A modern DBMS has the following characteristics:

###### Real-world entity: A modern DBMS is more realistic and uses real-world entities to design its architecture. 

###### Relation-based tables: DBMS allows entities and relations among them to form tables. 

###### Isolation of data and application: A database is an active entity, whereas data is said to be passive, on which the database works and organizes.

###### Less redundancy: DBMS follows the rules of normalization, which splits a relation when any of its attributes is having redundancy in values. 

###### Normalization: a mathematically rich and scientific process that reduces data redundancy.

###### Consistency: a state where every relation in a database remains consistent. A DBMS can provide greater consistency as compared to earlier forms of data storing applications like file-processing systems.

###### Query Language: DBMS is equipped with query language, which makes it more efficient to retrieve and manipulate data. 

###### ACID Properties: DBMS follows the concepts of Atomicity, Consistency, Isolation, and Durability (normally shortened as ACID). These concepts are applied on transactions, which manipulate data in a database. ACID properties help the database stay healthy in multi-transactional environments and in case of failure.

###### Multiuser and Concurrent Access: DBMS supports multi-user environment and allows them to access and manipulate data in parallel. Though there are restrictions on transactions when users attempt to handle the same data item, but users are always unaware of them.

###### Multiple views: DBMS offers multiple views for different users. A user who is in the Sales department will have a different view of database than a person working in the Production department. This feature enables the users to have a concentrate view of the database according to their requirements.

###### Security: Features like multiple views offer security to some extent where users are unable to access data of other users and departments. DBMS offers methods to impose constraints while entering data into the database and retrieving the same at a later stage. DBMS offers many different levels of security features, which enables multiple users to have different views with different features. For example, a user in the Sales department cannot see the data that belongs to the Purchase department. Additionally, it can also be managed how much data of the Sales department should be displayed to the user. Since a DBMS is not saved on the disk as traditional file systems, it is very hard for miscreants to break the code.

##### Administrators: Administrators maintain the DBMS and are responsible for administrating the database. They are responsible to look after its usage and by whom it should be used. They create access profiles for users and apply limitations to maintain isolation and force security. Administrators also look after DBMS resources like system license, required tools, and other software and hardware related maintenance.

##### Designers: Designers are the group of people who actually work on the designing part of the database. They keep a close watch on what data should be kept and in what format. They identify and design the whole set of entities, relations, constraints, and views.

##### End Users: End users are those who actually reap the benefits of having a DBMS. End users can range from simple viewers who pay attention to the logs or market rates to sophisticated users such as business analysts.
