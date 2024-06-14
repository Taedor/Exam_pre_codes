# Exam_pre_codes


## Способ как не создавать ненужные лишние окна:

код Window XAMl
```XAML
<Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Grid>
               <Grid.RowDefinitions>

           <RowDefinition Height="40*"/>

           <RowDefinition Height="177*"/>


       </Grid.RowDefinitions>

       <Grid.ColumnDefinitions>

           <ColumnDefinition Width="3*"/>

           <ColumnDefinition Width="13*"/>


       </Grid.ColumnDefinitions>

       <StackPanel x:Name="Menu_SP" Grid.Row="1" Grid.Column="0">

           <Label Content="MENU" 
          Foreground="#004572" FontSize="16"
          HorizontalAlignment="Center" />

           <Separator Margin="15" Background="White"/>

           <Button x:Name="btn_show_students"
           Width="120" Height="25"
           Content="Show Students"
           Foreground="#004572" FontSize="15" Click="btn_show_students_Click"
           />
           <Separator Margin="15" Background="White"/>

           <Button x:Name="btn_show_grades"
           Width="120" Height="25"
           Content="Show Grades"
           Foreground="#004572" FontSize="15" Click="btn_show_grades_Click"
           />

           <Separator Margin="15" Background="White"/>

           <Button x:Name="btn_show_exams"
           Width="120" Height="25"
           Content="Show Exams"
           Foreground="#004572" FontSize="15" Click="btn_show_exams_Click"
           />


           <Separator Margin="45" Background="White"/>

           <Button x:Name="btn_exit"
           Width="120" Height="25"
           Content="EXIT"
           Foreground="#004572" FontSize="15" Click="btn_exit_Click"
           />

       </StackPanel>


       <StackPanel x:Name="SP_Students" Grid.RowSpan="2" Grid.Column="1" Visibility="Collapsed">

           <Label Content="STUDENTS"
          FontSize="20" Foreground="#004572"
          HorizontalAlignment="Center"
          />

           <DataGrid x:Name="DG_Students" Height="318"/>

       </StackPanel>
    </Grid>
</Window>
```
## ОБЪЯСНЕНИЕ

```XAML
<Separator> - некий пробел между элементами. Настройка через Margin = " ".
И да, не забывайте в нем подгонять Background под фон того, на чем оно. Грид или StackPanel. По дефолту Separator имеет Белый цвет.
```
# **Как можно было замететь, я использую несколько "StackPanel". Это не запрещено и как раз выход для НЕ создания множества окон.**
```XAML
Visibility="Collapsed" 
``` 
# **только Collapsed вместо Hidden. С помощью кнопки меняем свойство. Ниже код**

```csharp
       private void btn_show_students_Click(object sender, RoutedEventArgs e)
       {
           if (SP_Students.Visibility == Visibility.Collapsed & SP_Grades.Visibility != Visibility.Visible & SP_Exams.Visibility != Visibility.Visible)
           {

               SP_Students.Visibility = Visibility.Visible;

           }
           else
           {
               SP_Students.Visibility = Visibility.Collapsed;
           }
       }
```
- как можно было замететь, то у меня несколько SP (StackPanel), и тут я проверяю НЕ видны ли они. Вот так легко меняется свойство.

# Но если уж так сильно любите окна, то вот код перемещения. Уникален для всех ОКОН
```C#
MenuScreen dashboard = new MenuScreen(); - где MenuScreen название Окна.
dashboard.Show();
this.Close();
```

## *Мой код (ГПТ) Логирования* 
```C#
SqlConnection sqlCon = new SqlConnection(@"Data Source=ИМЯ_СЕРВЕРА;Initial Catalog=ИМЯ_БАЗЫ;Integrated Security=True;Trust Server Certificate=True");
    try
    {
        if (sqlCon.State == ConnectionState.Closed)
            sqlCon.Open();
        String query = "SELECT * FROM SysLogin (SysLogin --> таблица) WHERE Login=@Login AND Password=@Password";
        SqlCommand sqlCmd = new SqlCommand(query, sqlCon);
        sqlCmd.CommandType = CommandType.Text;
        sqlCmd.Parameters.AddWithValue("@Login", txt_login.Text);
        sqlCmd.Parameters.AddWithValue("@Password", txt_passwd.Password);
        int role = Convert.ToInt32(sqlCmd.ExecuteScalar());
        switch (role)
        {
            case 1:
                MenuScreen dashboard = new MenuScreen();

                dashboard.Show();
                this.Close();
                MessageBox.Show("Access login. Welcome to back, Admin");
                break;

            default:
                MessageBox.Show("Username or Password is incorrect");
                break;
        }
    }

    catch (Exception ex)
    {
        MessageBox.Show(ex.Message);
    }
    finally
    {
        sqlCon.Close();
    }
}
```
