
# WPF 애플리케이션으로 짝맞추기 게임 만들기
![2024-12-01 15 50 22](https://github.com/user-attachments/assets/2cf6e572-f050-4afc-881f-817b3c1b7e63)


## 솔루션 탐색기
- MatchGame이라는 프로젝트 파일안에 여러가지의 구성 파일들이 존재한다.
- MainWindow.xaml => 창에 들어가는 모든 디자인 요소에 관련된 내용들이 들어 와있다. XAML코드가 창의 모습과 배치를 결정한다.
- MainWindow.xaml.cs => 코드숨김('뒤에 있는 코드'란 의미)파일이라고 부른다. 게임이 실행되는 방식을 결정하는 코드를 추가한다.


## XAML(eXtensible Application Markup Language)
- c# 개발자가 UI를 디자인할때 사용하는 마크업 언어이다.
<HTML언어와 유사하다>

```XAML
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


### c# 코드 구조(XAML 코드에 다음과 같이 연관성이 있다.)
 1. namespace MatchGame
```
x:Class="MatchGame.MainWindow"
```
 - 프로젝트의 이름으로 생각하면 된다.
 
 2. public partial Class MainWindow : Window
 - Microsoft Build Engine(MSBuild)은 Window에서 파생되는 partial 클래스를 ```x:Class``` 턱성에 지정하는 이름으로 생성한다.
 - 생성된 partial클래스는 InitializeComponent메서드를 구현하고 이 메서드를 통해 이벤트 등록, 속성 설정하기 위해 호출한다.

 - XAML코드의 ```x:Class="MatchGame.MainWindow"``` 특성으로 지정된 이름과 같은 이름을 가진 partical 클래스여야 하며 Window에서 파생되어야 한다.
 이를 통해 애플리케이션 빌드 시 태그 파일에 대해 생성 되는 partial 클래스와 코드 숨김 파일을 연결할수 있다.
 
 4. public MainWindow
```
 public MainWindow()
        {
            InitializeComponent();
            timer.Interval = TimeSpan.FromSeconds(.1);
            timer.Tick += Timer_Tick;
            SetUpGame();
        }
```

-  WPF 애플리케이션에서 자동으로 생성된 메서드 이며 UI 구성 요소를 초기화 하며, XAML파일에서 정의된 UI요소를 메모리에 로드한다. 이벤트 핸들러를 연결하는 작업도 수행한다.
- 0.1초마다 Tick 이벤트를 발생시키며 이로인해 Timver_Tick메서드를 호출한다. 
- SetUpGame()메서드를 호출하여여 통해 게임의 초기상태를 설정한다.

  
 5. Timver_Tick 메서드
```
    private void Timer_Tick(object? sender, EventArgs e)
        {
            tenthsOfSecondsElapsed++;
            TimeTextBlock.Text = (tenthsOfSecondsElapsed / 10F).ToString("0.0s");
            if (matchesFound == 8)
            {
                timer.Stop();
                TimeTextBlock.Text = TimeTextBlock.Text + "-play again?";
            }
        }
```

-  sender는 이벤트를 방생시킨 객체를 나타내며, e는 이벤트에 대한 추가 정보를 포함한다.
- tenthsOfSecondsElapsed변수를 1 증가시켜 경관된 시간을 추척한다.
- tenthsOfSecondsElapse를 10으로 나누어 초 단위로 변환한다.
- 이후 문자열로 변환후 TimeTextBlock의 텍스트 속성에 할당한다. 
- 8쌍의 쌍을 다 맞우면 timer를 멈추고 "-play agin?" 라는 문구를 띄운다.


 6. SetUpGame 메서드
```
   private void SetUpGame()
        {

            List<string> animalEmoji = new List<string>()
            {
                "A","A"
                ,"B","B"
                ,"C","C"
                ,"D","D"
                ,"E","E"
                ,"F","F"
                ,"G","G"
                ,"H","H"
            };
                Random random = new Random();
                foreach (TextBlock textBlock in mainGrid.Children.OfType<TextBlock>())
                {
                    if (textBlock.Name != "TimeTextBlock")
                    {
                        textBlock.Visibility = Visibility.Visible;
                        int index = random.Next(animalEmoji.Count);
                        string nextemoji = animalEmoji[index];
                        textBlock.Text = nextemoji;
                        animalEmoji.RemoveAt(index);
                    }
                }
            timer.Start();
            tenthsOfSecondsElapsed = 0;
            matchesFound = 0;
        }
```

- 8쌍의 문자를 List로 만든다
- Random 클래스를 사용하여 UI에 랜덤을 나타나게 배치한다.
- timer를 시작하여 게임이 시작되었다는것을 사용자에게 알려준다.
- tenthsOfSecondsElapsed변수에 0을 할당하여 0초부터 사용자가 볼수 있게끔 설정한다.
-  matchesFound에 0을 할당하여 이후 게임을 진행하면서 8이 되었을때 종료하기 위해 조건을 위해 만들어 졌다.



 7. TextBlock_MouseDown 이벤트 메서드
```
 private void TextBlock_MouseDown(object sender, MouseButtonEventArgs e)
        {
            TextBlock textBlock = sender as TextBlock;
            if (findingMatch == false)
            {
                textBlock.Visibility = Visibility.Hidden;
                lastTextBlockClicked = textBlock;
                findingMatch = true;
            }else if(textBlock.Text == lastTextBlockClicked.Text){
                matchesFound++;
                textBlock.Visibility = Visibility.Hidden;
                findingMatch = false;
            }
            else
            {
                lastTextBlockClicked.Visibility = Visibility.Visible;
                findingMatch = false;
            }
        }
```

- 마우스 클릭 시 UI에서 선택되어진 항목을 숨겨 놓는다.
- 마우스 클릭을 이용해 동일한 짝을 클릭할경우 종료에 맞는 조건 달성을 위해 matchesFound변수에 1을 추가한다.
- 동일하지 않은 짝을 클릭할 경우 숨겨놓은 항목을 보이게 한다.

 
 8. TimeTextBlock_MouseDown 이벤트 메서드
```
     private void TimeTextBlock_MouseDown(object sender, MouseButtonEventArgs e)
        {
            if(matchesFound == 8)
            {
                SetUpGame();
            }
        }
```

 - 게임이 끝난후 "TimeTextBlock"을 클릭할경우 다시 게임을 시작한다.
 
 9. 필드에 존재 하는 변수(필드: 클래스 안에서 정의 되지만 메서드 밖에 있는 구역)
```
        TextBlock lastTextBlockClicked;
        bool findingMatch = false;
```

