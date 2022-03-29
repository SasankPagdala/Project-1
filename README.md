# StudentDataBase

package com.sasank;
import org.w3c.dom.ls.LSOutput;

import java.util.Scanner;

public class Student {
    private String firstName;
    private String lastName;
    private int gradeYear;
    private String studentID;
    private String courses = "";
    private int tuitionBalance = 0;
    private static int costOfCourse = 600;
    private static int id = 1000;

    //Constructor: Prompts the user to enter student's name and year
    public Student() {
        Scanner in = new Scanner(System.in);
        System.out.print("Enter Student First Name: " );
        this.firstName = in.nextLine();

        System.out.print("Enter Student Last Name: " );
        this.lastName = in.nextLine();

        System.out.println("1 - Freshman\n2 - Sophmore\n3 - Junior\n4 - Senior\nEnter Student Class Level: " );
        this.gradeYear = in.nextInt();

        setStudentID();
    }

    //Generate an ID:
    private void setStudentID() {
        //Grade Level + ID
        id++;
        this.studentID = gradeYear + "" + id;

    }
    //Enroll in courses
    public void enroll() {
        //Get inside a loop, user hits 0
        do {
            System.out.print("Enter course to enroll(Q to quit): ");
            Scanner in = new Scanner(System.in);
            String course = in.nextLine();
            if (!course.equals("Q")) {
                courses = courses + "\n " + course;
                tuitionBalance = tuitionBalance + costOfCourse;
            }
            else {
                break;
            }
        }while (1 != 0);
    }
    //View Balance
    public void viewBalance(){
        System.out.println("Your balance is: $" + tuitionBalance);
    }

    //Pay Tuition
    public void payTuition() {
        viewBalance();
        System.out.print("Enter your payment: $");
        Scanner in = new Scanner(System.in);
        int payment = in.nextInt();
        tuitionBalance = tuitionBalance - payment;
        System.out.println("Thank you for your payment of $" + payment);
        viewBalance();
    }

    //Show status
    public String toString() {
        return "Name: " + firstName + " " + lastName +
                "\nGrade Lavel: " + gradeYear +
                "\nStudentID: " +studentID +
                "\nCourses Enrolled:" + courses +
                "\nBalance: $" + tuitionBalance;
    }
}


//STUDENT DATABASE APP DIFFERENT CLASS\\

package com.sasank;

import java.util.Scanner;

public class StudentDatabaseApp {

    public static void main(String[] args) {
        Student stu1 = new Student();
        stu1.enroll();
        stu1.payTuition();
        System.out.println(stu1.toString());

        // Ask how many new students we want to add
        System.out.println("Enter a new number of new students to enroll: ");
        Scanner in = new Scanner(System.in);
        int numOfStudents = in.nextInt();
        Student[] students = new Student[numOfStudents];

        //Create n number of new students
        for (int n = 0;n <numOfStudents; n++ ) {
            students[n] = new Student();
            students[n].enroll();
            students[n].payTuition();
        }
        for (int n = 0;n <numOfStudents; n++ ) {
            System.out.println(students[n].toString());
        }
    }
}

