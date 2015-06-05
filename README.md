# Teachers-App
This application is built in Visual Basic and is a teachers best friend. This program pulls information from a file, sets the information into a table, and calculates the mean of an entire class.
//A txt file must be created with a list of grades going down in a row//

Public Class frmgrades

    Dim totalgrade As Double
    Dim count As Integer
    Dim totalvalue As Double
    Dim variance As Double
    Dim standarddev As Double
    Dim mean As Double
    Dim letter As String
    Dim grade As String


    Private Sub cmdcompute_Click(sender As System.Object, e As System.EventArgs) Handles cmdcompute.Click
        Dim sr As IO.StreamReader = IO.File.OpenText("grades.txt")
        Dim sr2 As IO.StreamReader = IO.File.OpenText("grades.txt")
        Dim sr3 As IO.StreamReader = IO.File.OpenText("grades.txt")

        Dim fmtStr As String = "{0,10}{1,8:N0}"
        Dim fmtStr2 As String = "{0,10}{1,2:N0}{2,4}"

        lstgrades.Items.Clear()
        'lstgrades.Items.Add(String.Format(fmtStr, "There were ", "exams.", "Mean: ", "Std. Deviation: "))



        Do While sr.Peek <> -1

            grade = CInt(sr.ReadLine)

            totalgrade = totalgrade + grade

            count = count + 1
        Loop

        mean = totalgrade / count

        lstgrades.Items.Add(String.Format(fmtStr2, "There were ", count, " exams taken."))
        lstgrades.Items.Add(String.Format(fmtStr, "Mean: ", CStr(mean)))



        sr.Close()

        Do While sr2.Peek <> -1

            grade = CInt(sr2.ReadLine)

            totalvalue = totalvalue + ((grade - mean) * (grade - mean))

        Loop

        variance = totalvalue / count

        standarddev = Math.Sqrt(variance)

        lstgrades.Items.Add(String.Format(fmtStr, "Std. Dev. ", CStr(standarddev)))

        sr2.Close()

        Do While sr3.Peek <> -1

            grade = CInt(sr3.ReadLine)



            If (grade > 89.1) Then
                letter = "A"
            ElseIf (grade > 76) Then
                letter = "B"
            ElseIf (grade > 64) Then
                letter = "C"
            ElseIf (grade > 51) Then
                letter = "D"
            Else
                letter = "F"
            End If

            lstgrades.Items.Add(String.Format(fmtStr, CStr(grade), letter))

        Loop

        'CStr(totalvalue), CStr(mean)

        sr3.Close()

    End Sub
End Class
