
# WPF 어플리케이션으로 짝맞추기 게임 만들기
![2024-12-01 15 50 22](https://github.com/user-attachments/assets/2cf6e572-f050-4afc-881f-817b3c1b7e63)


## 솔루션 탐색기
- MatchGame이라는 프로젝트 파일안에 여러가지의 구성 파일들이 존재한다.
- MainWindow.xaml => 창에 들어가는 모든 디자인 요소에 관련된 내용들이 들어 와있다. XAML코드가 창의 모습과 배치를 결정한다.
- MainWindow.xaml.cs => 코드숨김('뒤에 있는 코드'란 의미)파일이라고 부른다. 게임이 실행되는 방식을 결정하는 코드를 추가한다.


## XAML(eXtensible Application Markup Language)
- c# 개발자가 UI를 디자인할때 사용하는 마크업 언어이다.
<HTML언어와 유사하다>

```XAMK
<Window x:Class="MatchGame.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:MatchGame"
        mc:Ignorable="d"
        Title="Find all of the matching animals" Height="643" Width="818">
        <Grid x:Name="mainGrid">
                <Grid.ColumnDefinitions>        
                <ColumnDefinition />
                <ColumnDefinition />
                <ColumnDefinition/>
                <ColumnDefinition />  
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition />
                <RowDefinition />
                <RowDefinition />
                <RowDefinition />
        </Grid.RowDefinitions>
                <TextBlock Grid.Column="0" HorizontalAlignment="Center" Grid.Row="0" Text="?" VerticalAlignment="Center" Margin="0,0,0,0" FontSize="36" TextWrapping="Wrap" MouseDown="TextBlock_MouseDown"/>
                <TextBlock Grid.Column="1" HorizontalAlignment="Center" Grid.Row="0" Text="?" VerticalAlignment="Center" Margin="0,0,0,0" FontSize="36" TextWrapping="Wrap" MouseDown="TextBlock_MouseDown"/>
                ........
                <TextBlock Grid.Column="3" HorizontalAlignment="Center" Grid.Row="3" Text="?" VerticalAlignment="Center" Margin="0,0,0,0" FontSize="36" TextWrapping="Wrap" MouseDown="TextBlock_MouseDown"/>
                <TextBlock x:Name="TimeTextBlock" HorizontalAlignment="Center" Grid.Row="4" Text="Elapse time" VerticalAlignment="Center" Grid.ColumnSpan="4" FontSize="36" MouseDown="TimeTextBlock_MouseDown" TextWrapping="Wrap"/>
        </Grid>
</Window>
```


## c# 코드
![image](https://github.com/user-attachments/assets/469cf71e-a42d-4f84-8514-3fc091f93ca4)


### c# 코드 구조
 1. namespace MatchGame
  -> 프로젝트 이름과 동일
 2. Class MainWindow
 3. public MainWindow
 4. Timver_Tick 메서드
 5. SetUpGame 메서드
 6. TextBlock_MouseDown 이벤트 메서드
 7. TimeTextBlock_MouseDown 이벤트 메서드
 8. 필드에 존재 하는 변수(필드: 클래스 안에서 정의 되지만 메서드 밖에 있는 구역)


