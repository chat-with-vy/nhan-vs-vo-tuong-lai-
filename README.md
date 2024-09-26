;> code c# mấy bt cũng hay phếch e<br>
![image](https://github.com/user-attachments/assets/8b077e5a-973b-4602-b0ab-d4321f3a7a33)<br>
;> lên mạng copy past mấy cái tên môn học rồi copy tên sinh viên lun e đỡ bịa<br>
;> bài này a viết gọn lắm cỡ 500 dòng á<br>
;> này phần xử lý logic, ó ngắn gọn dễ hỉu lun e
```
private static void CreateFakeRegisters(List<Register> registers, List<Student> students, List<Subject> subjects)
{
    DateTime currentTime = DateTime.Now;

    registers.Add(new Register(students[0], subjects[0]) { RegisterTime = currentTime.AddMinutes(1) });
    registers.Add(new Register(students[1], subjects[0]) { RegisterTime = currentTime.AddMinutes(2) });
    registers.Add(new Register(students[2], subjects[0]) { RegisterTime = currentTime.AddMinutes(3) });
    registers.Add(new Register(students[3], subjects[0]) { RegisterTime = currentTime.AddMinutes(4) });
    registers.Add(new Register(students[4], subjects[0]) { RegisterTime = currentTime.AddMinutes(5) });
    registers.Add(new Register(students[0], subjects[5]) { RegisterTime = currentTime.AddMinutes(6) });
    registers.Add(new Register(students[1], subjects[2]) { RegisterTime = currentTime.AddMinutes(7) });
    registers.Add(new Register(students[2], subjects[1]) { RegisterTime = currentTime.AddMinutes(8) });
    registers.Add(new Register(students[3], subjects[3]) { RegisterTime = currentTime.AddMinutes(9) });
    registers.Add(new Register(students[4], subjects[4]) { RegisterTime = currentTime.AddMinutes(10) });
    registers.Add(new Register(students[1], subjects[1]) { RegisterTime = currentTime.AddMinutes(11) });
    registers.Add(new Register(students[1], subjects[5]) { RegisterTime = currentTime.AddMinutes(12) });
    registers.Add(new Register(students[0], subjects[1]) { RegisterTime = currentTime.AddMinutes(13) });
    registers.Add(new Register(students[0], subjects[2]) { RegisterTime = currentTime.AddMinutes(14) });
    registers.Add(new Register(students[0], subjects[3]) { RegisterTime = currentTime.AddMinutes(15) });
}

private static void CreateFakeSubjects(List<Subject> subjects)
{
    subjects.Add(new Subject("C++", 3, 36));
    subjects.Add(new Subject("C", 3, 36));
    subjects.Add(new Subject("C#", 4, 48));
    subjects.Add(new Subject("Java", 4, 46));
    subjects.Add(new Subject("Kotlin", 3, 36));
    subjects.Add(new Subject("Android", 5, 60));
    subjects.Add(new Subject("SQL", 3, 36));
    subjects.Add(new Subject("Python", 4, 48));
    subjects.Add(new Subject("JavaScript", 3, 36));
    subjects.Add(new Subject("Web design", 2, 25));
}
private static void CreateFakeStudents(List<Student> students)
{
    students.Add(new Student("Trần Văn Nam", "CNTT"));
    students.Add(new Student("Ngô Văn Tài", "CNTT"));
    students.Add(new Student("Hồ Hoàng Yến", "CNTT"));
    students.Add(new Student("Võ Hoàng Yến", "CNTT"));
    students.Add(new Student("Vy Thị Yến", "CNTT"));
    students.Add(new Student("Mai Văn Dũng", "CNTT"));
    students.Add(new Student("Lê Thanh Thảo", "CNTT"));
    students.Add(new Student("Ngô Nhật Phong", "CNTT"));
    students.Add(new Student("Ma Thanh Thức", "CNTT"));
    students.Add(new Student("Khúc Thị Lệ Quyên", "CNTT"));
    students.Add(new Student("Trương Trọng Anh", "CNTT"));
    students.Add(new Student("Nguyễn Quỳnh Anh", "CNTT"));
    students.Add(new Student("Thân Văn Huấn", "CNTT"));
}

private static void AddStudent(List<Student> students)
{
    Console.WriteLine("Họ tên: ");
    string fullName = Console.ReadLine();
    Console.WriteLine("Chuyên nghành: ");
    string major = Console.ReadLine();

    Student student = new Student(fullName, major);
    students.Add(student);
    Console.WriteLine("====> Tạo thành công");
}

private static void AddSubject(List<Subject> subjects)
{
    Console.WriteLine("Tên môn: ");
    string name = Console.ReadLine();
    Console.WriteLine("Số chỉ: ");
    int credit = int.Parse(Console.ReadLine());
    Console.WriteLine("Số tiết: ");
    int numOfLesson = int.Parse(Console.ReadLine());
    Subject subject = new Subject(name, credit, numOfLesson);
    subjects.Add(subject);
    Console.WriteLine("====> Tạo thành công");

}
private static void AddRegister(List<Register> registers, List<Student> students, List<Subject> subjects)
{
    if (students.Count == 0 || subjects.Count == 0)
    {
        Console.WriteLine("Sinh viên hoặc môn học chưa được thêm");
        return;
    }

    Console.WriteLine("Danh sách sinh viên:");
    for (int i = 0; i < students.Count; i++)
    {
        Console.WriteLine($"{i + 1}. {students[i].FullName}");
    }
    int studentIndex = int.Parse(Console.ReadLine()) - 1;


    Console.WriteLine("Danh sách môn học: ");
    for (int i = 0; i < subjects.Count; i++)
    {
        Console.WriteLine($"{i + 1}. {subjects[i].SubjectName}");
    }
    int subjectIndex = int.Parse(Console.ReadLine()) - 1;


    if (students[studentIndex].Registrations.Count >= 8)
    {
        Console.WriteLine("Sv này đã đk đủ 8 môn học");
        return;
    }


    var registered = registers.Exists(r => r.Student == students[studentIndex]);
    if (registered)
    {
        Console.WriteLine($"SV đã đk môn học '{subjects[subjectIndex].SubjectName}' này rồi");
        return;
    }

    Register register = new Register(students[studentIndex], subjects[subjectIndex]);
    registers.Add(register);
    Console.WriteLine("====> Tạo thành công");

}
private static void DisplayStudents(List<Student> students)
{
    Console.WriteLine($"{"Mã SV",-10}{"Họ tên",-20}{"Chuyên nghành",-15}");
    Console.WriteLine(new string('-', 45));
    foreach (var item in students)
    {
        Console.WriteLine(item);
    }
}
private static void DisplaySubjects(List<Subject> subjects)
{
    Console.WriteLine($"{"Mã môn",-10}{"Tên môn",-15}{"Tín chỉ",-10}{"Số tiết",-10}");
    Console.WriteLine(new string('-', 45));
    foreach (var item in subjects)
    {
        Console.WriteLine(item);
    }
}
private static void DisplayRegister(List<Register> registers)
{
    Console.WriteLine($"{"Mã ĐK",-10}{"Mã SV",-10}{"Họ tên",-20}{"Mã môn",-10}" +
        $"{"Tên môn",-15}{"Thời gian ĐK",-15}");
    Console.WriteLine(new string('-', 80));
    foreach (var item in registers)
    {
        Console.WriteLine(item);
    }
}
private static void SortByName(List<Student> students)
{
    students.Sort((s1, s2) =>
    {
        var first = s1.FullName.FirstName.CompareTo(s2.FullName.FirstName);
        if (first != 0)
        {
            return first;
        }
        return s1.FullName.LastName.CompareTo(s2.FullName.LastName);
    });
}
private static void SortByCredit(List<Subject> subjects)
{
    subjects.Sort((s1, s2) => s2.Credit.CompareTo(s1.Credit));
}
private static void SortByRegTime(List<Register> registers)
{
    registers.Sort((r1, r2) => r1.RegisterTime.CompareTo(r2.RegisterTime));
}
private static void SortRegisterByStudentId(List<Register> registers)
{
    registers.Sort((r1, r2) => r1.Student.StudentId.CompareTo(r2.Student.StudentId));
}
private static void SortRegisterBySubjectId(List<Register> registers)
{
    registers.Sort((r1, r2) => r1.Subject.SubjectId.CompareTo(r2.Subject.SubjectId));
}
private static List<Register> FindRegistersByStudentId(List<Register> registers)
{
    Console.WriteLine("Mã SV: ");
    string studentId = Console.ReadLine();
    return registers.FindAll(s => s.Student.StudentId == studentId);
}
private static List<Register> FindRegistersBySubjectId(List<Register> registers)
{
    Console.WriteLine("Mã môn: ");
    int subjectId = int.Parse(Console.ReadLine());
    return registers.FindAll(s => s.Subject.SubjectId == subjectId);
}
private static void EditStudentInfo(List<Student> students)
{
    Console.WriteLine("Mã SV: ");
    string studentId = Console.ReadLine();
    foreach (var item in students)
    {
        if (item.StudentId == studentId)
        {
            Console.WriteLine("Họ tên: ");
            item.FullName = new FullName(Console.ReadLine());
            Console.WriteLine("Chuyên nghành: ");
            item.Major = Console.ReadLine();
            Console.WriteLine("====> Đã cập nhật");
            return;
        }
    }

    Console.WriteLine("Sv ko tồn tại");
}
private static void EditSubjectLesson(List<Subject> subjects)
{
    Console.WriteLine("Mã môn: ");
    int subjectId = int.Parse(Console.ReadLine());
    foreach (var item in subjects)
    {
        if (item.SubjectId == subjectId)
        {
            Console.WriteLine("Số tiết: ");
            item.NumOfLesson = int.Parse(Console.ReadLine());
            Console.WriteLine("====> Đã cập nhật");
            return;
        }
    }
    Console.WriteLine("Môn học ko tồn tại");
}
private static void RemoveSubject(List<Subject> subjects)
{
    Console.WriteLine("Mã môn: ");
    int subjectId = int.Parse(Console.ReadLine());
    Console.WriteLine("Bạn có chắc muốn xóa (Y/N)?");
    if (Console.ReadLine().Trim().ToLower() == "y")
    {
        int removed = subjects.RemoveAll(s => s.SubjectId == subjectId);
        Console.WriteLine(removed > 0 ? "Xóa thành công" : "Xóa thất bại");
    }
    else
    {
        Console.WriteLine("Hủy xóa");
    }
}
private static void RemoveStudent(List<Student> students)
{
    Console.WriteLine("Mã SV: ");
    string studentId = Console.ReadLine();
    Console.WriteLine("Bạn có chắc muốn xóa (Y/N)?");
    if (Console.ReadLine().Trim().ToLower() == "y")
    {
        int removed = students.RemoveAll(s => s.StudentId == studentId);
        Console.WriteLine(removed > 0 ? "Xóa thành công" : "Xóa thất bại");
    }
    else
    {
        Console.WriteLine("Hủy xóa");
    }
}
private static void RemoveRegister(List<Register> registers)
{
    Console.WriteLine("Mã ĐK: ");
    int registerId = int.Parse(Console.ReadLine());
    Console.WriteLine("Bạn có chắc muốn xóa (Y/N)?");
    if (Console.ReadLine().Trim().ToLower() == "y")
    {
        int removed = registers.RemoveAll(s => s.RegisterId == registerId);
        Console.WriteLine(removed > 0 ? "Xóa thành công" : "Xóa thất bại");
    }
    else
    {
        Console.WriteLine("Hủy xóa");
    }
}
```
;> a mới fix lại hàm này tý cho hợp lý nà<br>
```
private static void AddRegister(List<Register> registers, List<Student> students, List<Subject> subjects)
{
    if (students.Count == 0 || subjects.Count == 0)
    {
        Console.WriteLine("Sinh viên hoặc môn học chưa được thêm");
        return;
    }

    Console.WriteLine("Mã SV: ");
    string studentId = Console.ReadLine();
    var student = students.FirstOrDefault(s => s.StudentId == studentId);
    if (student == null)
    {
        Console.WriteLine("SV ko tồn tại");
        return;
    }


    Console.WriteLine("Danh sách môn học: ");
    for (int i = 0; i < subjects.Count; i++)
    {
        Console.WriteLine($"{i + 1}. {subjects[i].SubjectName}");
    }
    int subjectIndex = int.Parse(Console.ReadLine()) - 1;


    if (student.Registrations.Count >= 8)
    {
        Console.WriteLine("Sv này đã đk đủ 8 môn học");
        return;
    }


    var registered = registers.Exists(r => r.Student == student);
    if (registered)
    {
        Console.WriteLine($"SV đã đk môn học '{subjects[subjectIndex].SubjectName}' này rồi");
        return;
    }

    Register register = new Register(student, subjects[subjectIndex]);
    registers.Add(register);
    Console.WriteLine("====> Tạo thành công");

}
```
;> à fix lại xíu e
```
var registered = registers.Exists(s => s.Student == student && s.Subject == subjects[subjectIndex]);
if (registered)
{
    Console.WriteLine("SV đã đăng kí môn này rồi");
}
```
;> chắc vầy oki rồi<br>
;> à chưa oki e<br>
```
var registered = registers.Exists(s => s.Student == student && s.Subject == subjects[subjectIndex]);
if (registered)
{
    Console.WriteLine($"SV đã đăng kí môn '{subjects[subjectIndex].SubjectName}' này rồi");
    return;
}
```
=)) quên return
```
;> fix lại hàm này nữa, xóa môn học thì phải xóa ở bảng sv đã đk môn học đó lun<br>
```
private static void RemoveSubject(List<Subject> subjects,List<Register>registers)
{
    Console.WriteLine("Mã môn: ");
    int subjectId = int.Parse(Console.ReadLine());
    Console.WriteLine("Bạn có chắc muốn xóa (Y/N)?");
    if (Console.ReadLine().Trim().ToLower() == "y")
    {
        // Xóa tất cả bản đăng ký của môn học
        registers.RemoveAll(r => r.Subject.SubjectId == subjectId);

        int removed = subjects.RemoveAll(s => s.SubjectId == subjectId);
        Console.WriteLine(removed > 0 ? "Xóa thành công" : "Xóa thất bại");
    }
    else
    {
        Console.WriteLine("Hủy xóa");
    }
}
```
;> các list đã đk của sv phải đc thêm vô, để tăng cho đến khi bé hơn 8 môn học
```
if (student.Registrations.Count >= 8)
    {
        Console.WriteLine("SV đã đk đủ 8 môn học");
        return;
    }
```
```
private static void AddRegister(List<Register> registers, List<Student> students, List<Subject> subjects)
{
    if (students.Count == 0 || subjects.Count == 0)
    {
        Console.WriteLine("Sinh viên hoặc môn học phải được tạo trước");
        return;
    }

    Console.WriteLine("Mã SV: ");
    string studentId = Console.ReadLine();
    var student = students.FirstOrDefault(s => s.StudentId == studentId);
    if (student == null)
    {
        Console.WriteLine("SV ko tồn tại");
        return;
    }

    if (student.Registrations.Count >= 8)
    {
        Console.WriteLine("SV đã đk đủ 8 môn học");
        return;
    }


    Console.WriteLine("Danh sách các môn học:");
    for (int i = 0; i < subjects.Count; i++)
    {
        Console.WriteLine($"{i + 1}. {subjects[i].SubjectName}");
    }
    int subjectIndex = int.Parse(Console.ReadLine()) - 1;

    var registered = registers.Exists(s => s.Student == student && s.Subject == subjects[subjectIndex]);
    if (registered)
    {
        Console.WriteLine($"SV đã đăng kí môn '{subjects[subjectIndex].SubjectName}' này rồi");
        return;
    }

    Register register = new Register(student, subjects[subjectIndex]);
    registers.Add(register);
    student.Registrations.Add(register);


    Console.WriteLine("====> Tạo thành công");

}
```
=)) viết bt chơi chơi mà bug nhìu
