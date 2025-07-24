controller .java:
 

 package edu.mrk.studentproject.student.controller;
import java.util.List;

import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import edu.mrk.studentproject.student.models.Student;
import edu.mrk.studentproject.student.services.StudentServices;
@RestController
@RequestMapping("/student/api")
public class StudentController {
private StudentServices service;

	public StudentController() {
	super();
	// TODO Auto-generated constructor stub
	service = new StudentServices();
	}
	  @GetMapping("/title")
	  public String displayvalue(){
	    return "Welcome to Student Information";
	  }
	@GetMapping("/students")
	public List<Student> readStudents(){
	return service.readStudents();
	}
	  @PostMapping("/create")
	  public String createStudents(@RequestBody Student student){
	    service.createStudent(student);
	    return "Student information created Successfully";
	  }
	  @PutMapping("/update")
	  public String updateStudent(@RequestBody Student student){
	    service.updateStudent(student);
	    return "Student information updated succesfully";
	  }
	  @DeleteMapping("/delete")
	  public String deleteStudent(@RequestBody Long id){
	    service.deleteStudent(id);
	    return "Student information deleted successfully";
	  }
	  @GetMapping("/student")
	  public Student readStudent(@RequestBody Long id){
	    return service.readStudent(id);
	  }
	}

student.java:


package edu.mrk.studentproject.student.models;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name="book")
public class Student {
@Id
@GeneratedValue(strategy=GenerationType.IDENTITY)
private Long id;
private String name;
private String department;
private Double marks;



public Student() {
	super();
	// TODO Auto-generated constructor stub
}
public Student(String name, String department, Double marks) {
super();
this.name = name;
this.department = department;
this.marks = marks;
}
public Student(Long id, String Name, String Department, Double Marks) {
super();
this.id = id;
this.name = Name;
this.department = Department;
this.marks = Marks;
}
public Long getId() {
return id;
}
public void setId(Long id) {
this.id = id;
}
public String getName() {
return name;
}
public void setName(String name) {
this.name = name;
}
public String getDepartment() {
return department;
}
public void setDepartment(String department) {
this.department = department;
}
public Double getMarks() {
return marks;
}
public void setMarks(Double marks) {
this.marks= marks;
}
}
 student CRud.java :


 package edu.mrk.studentproject.student.models;
import java.util.List;


public interface StudentCRUD {
	public void createStudent(Student student);
	public List<Student> readStudents();
	public void updateStudent(Student student);
	public void deleteStudent(Long id);
	public Student readStudent(Long id);
	}

studentRepository :


package edu.mrk.studentproject.student.repository;
import java.util.ArrayList;
import java.util.List;
import edu.mrk.studentproject.student.models.Student;

import edu.mrk.studentproject.student.models.StudentCRUD;

public class StudentRepository implements StudentCRUD{
private List<Student> students=null;
	public StudentRepository() {
	super();
	// TODO Auto-generated constructor stub
    students = new ArrayList<>();
    students.add(new Student(1L,"AAA","Cse",98.00));
    students.add(new Student (2L,"BBB","Cse",99.00));
    students.add(new Student(3L,"CCC","Cse",98.00));
    students.add(new Student(4L,"DDD","Cse",95.00));
	}

	@Override
	public void createStudent(Student student) {
	students.add(student);

	}

	@Override
	public List<Student> readStudents() {

	return students;
	}

	@Override
	public void updateStudent(Student student) {
	int index =0;
	  for(int i=0;i<students.size();i++){
	    if(students.get(i).getId() == student.getId()){
	      index = i;
	    }
	  }
	  students.set(index,student);

	}

	@Override
	public void deleteStudent(Long id) {
	int index =0;
	  for(int i=0;i<students.size();i++){
		  if(students.get(i).getId() == id){
	      index = i;
	    }
	  }
	  students.remove(index);

	}

	@Override
	public Student readStudent(Long id) {
	int index =0;
	  for(int i=0;i<students.size();i++){
	    if(students.get(i).getId() == id){
	      index = i;
	    }
	  }
	  return students.get(index);
	}

	}


studentservices :


package edu.mrk.studentproject.student.services;
import java.util.List;

import edu.mrk.studentproject.student.models.Student;
import edu.mrk.studentproject.student.repository.StudentRepository;


public class StudentServices {

private StudentRepository repo = null;

public StudentServices() {
super();
// TODO Auto-generated constructor stub
repo= new StudentRepository();
}
public List<Student> readStudents(){
return repo.readStudents();
}
  public void createStudent(Student student){
    repo.createStudent(student);
  }
  public void updateStudent(Student student){
    repo.updateStudent(student);
  }
  public void deleteStudent(Long id){
    repo.deleteStudent(id);
  }
  public Student readStudent(Long id){
    return repo.readStudent(id);
  }

}




If any of the projects above is able to help you out, please do click on "Star" on top right-hand-site. Thank you!
# java
java springboot
