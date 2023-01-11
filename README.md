# swiftUI



- [기초잡기](https://github.com/kimchulyeon/swiftUIStudy#-기초잡기)
  - [Text()](https://github.com/kimchulyeon/swiftUIStudy#-text)  
  - [Color()](https://github.com/kimchulyeon/swiftUIStudy#-color)  
  - [Materials()](https://github.com/kimchulyeon/swiftUIStudy#-materials)  
  - [Image()](https://github.com/kimchulyeon/swiftUIStudy#-image)  
  - [SF Symbol()](https://github.com/kimchulyeon/swiftUIStudy#-sf-symbol)  
  - [Label + Image](https://github.com/kimchulyeon/swiftUIStudy#-sf-symbol)  
  - [Event Modifier](https://github.com/kimchulyeon/swiftUIStudy#-event-modifier)  
  - [Custom Event Modifier](https://github.com/kimchulyeon/swiftUIStudy#-custom-event-modifier)  

- [실전](https://github.com/kimchulyeon/swiftUIStudy#-실전)  
  - [텍스트 띄워보기](https://github.com/kimchulyeon/swiftUIStudy#-텍스트-띄워보기)  
  - [subView로 분리](https://github.com/kimchulyeon/swiftUIStudy#-subView로-분리)  
  - [NavigationView](https://github.com/kimchulyeon/swiftUIStudy#-navigationview)  
  - [List](https://github.com/kimchulyeon/swiftUIStudy#-list)

<br />

## 🥑 기초잡기

<br />

### Text()

```
let number: Float = 30.9023

Text(number.formatted(.currency(code: "USD")))  $30.9023
Text(Date().formatted(date: .abbreviated, time: .omitted))  Sep 19, 2022
Text(Date(), style: .timer)

// 📌 modifier : ⭐️ cmd + 클릭 => Show SwiftUI Inspector ⭐️
Text("Hello World")
  .font(.largeTitle)
  .font(Font.system(size:))
  .font(Font.custom("Georgia" ,size:))
  .fontWeight(.regular)
  .foregroundColor(Color(hue: 1.0, saturation: 0.733, brightness: 0.842))
  .background(Color.gray)
  .background(Color.gray.gradient)
  .border(Color.yellow, width: 10)
  .cornerRadius(20)
  .overlay(Color(red: 1, green: 1, blud: 0.3, opacity: 0.2).frame(width: 160, hegith: 40)).frame(width: height: alignment:)
  .padding(24)
  .padding(EdgeInsets(top: leading: bottom: trailing:))
  .padding([.leading, .bottom], 50)
  .underline()
  .shadow(color: Color.gray, radius: 1, x: 1, y: 1)
  .multilineTextAlignment(.center)
  .lineSpaceing(5)
  .textSelection(.enabled)
  .truncationMode(.tail)
```


<br />

### Color()
```
Color(red: 0.9, green: 0.5, blue: 0.2)
Color("MyColorAtAssets")
Color(red: 100/255, green: 200/255, blue: 250/255)
  .frame(width: 250, height: 100)

Text()
  .background(Color.gray)
  .background(Color.gray.gradient)
  .border(Color.yellow, width: 10)
  .cornerRadius(20)
  .overlay(Color(red: 1, green: 1, blud: 0.3, opacity: 0.2).frame(width: 160, hegith: 40)).frame(width: height: alignment:)
```

<br />

### Materials()
```
Text("Hello World")
  .background(.thickMaterial)
```

<br />

### Image()
```
Image("myImgAtAssets")
  .frame(width: 250, height: 100)
  .clipped() // frame 크기 만큼만의 이미지를 잘라서 보여준다.
  .resizable() // frame 크기에 맞게 이미지 크기를 조절한다. (이미지가 찌그러지고 왜곡될 수 있다)
  .aspectRatio(contentMode: .fill)
  .scaledToFill()
  .clipped
  .aspectRatio(contentMode: .fit)
  .scaledToFit()
  .scaleEffect(CGSize(width: 0.5, height: 0.5))
  .blur(radius: 5)

// 📌 접근성 설정으로 폰트를 키우면 사이즈도 키워짐
@ScaledMetric var customSize: CGFloat = 100

Image("myImg")
  .frame(width: customSize, height: customSize)
```

<br />

### SF Symbol
```
Image(systemName: "house")
  .font(Font.system(size: 100).weight(.semibold))
  .symbolVariant(.fill)
  .symbolRenderingMode(.multicolor)
  .foregroundStyle(.red, .blue)
  .imageScale(.large)

Image(systemName: "dot.radiowaves.forward", variableValue: 0.8)
```

<br />

### Label + Image
```
Label("hello world", systemImage: "envelope.circle")
  .font(.largeTitle)
  .labelStyle(.titleAndIcon)
  .imageScale(.large)
```

<br />

### Event Modifier
onAppear()

onDisappear()

등등
```
Image(systemName: "envelope.circe")
  .onAppear(perform: {
    print("Image is shown")
  })
  .onDisappear(perform: {
    print("Image is gone")
  })
```

<br />

### Custom Event Modifier

📌 ViewModifier 프로토콜

반복적인 것들을 미리 struct로 구현해놓고 갖다쓰면 될듯
```
struct MyModifiers: ViewModifier {
  func body(content: Content)  -> some View {
    content
      .font(Font.system(size: 100).weight(.semibold))
      .foregroundColor(Color.blue)
  }
}

Image(systemName: "envelope.circle")
  .modifier(MyModifiers())




// 📌 init과 ViewModifier
struct MyModifiers: ViewModifier {
  var size: CGFloat

  init(size: CGFloat) {
    self.size = size
  }

  func body(content: Content) -> some View {
    content
      .font(Font.system(size: size).weight(.semibold))
  }
}

Image(systemName: "envelope.circle")
  .modifier(MyModifiers(size: 50))

```
<br />

### safe area ignore

```
VStack {
  ...
}
  .ignoresSafeArea(.all)
  .ignoresSafeArea(.container)
  .ignoresSafeArea(.keyboard)

  .ignoresSafeArea(.keyboard, edges: .top) // .bottom , .leading , .trailing , .all
```

<br />

### safe area modifier

```
VStack {
  ...
}

.safeAreaInset(edge: .bottom, content: {
  HStack {
    Spacer()
    Text("safe area bottom area").padding()
    Spacer()
  }
    .background(.yellow)
})
```
<br />

### priority 우선순위

폭이 컨텐츠보다 좁아서 ...으로 텍스트가 축소된다.

.layoutPriority(Double)

.fixedSize(horizontal: Bool, vertiacl: Bool)
```
HStack {
  Test("Hello World")
    .font(.title)
    .lineLimit(1)
  Image(systemName: "cloud")
    .font(.system(size: 80))
  Text("Hello Swift")
    .font(.title)
    .lineLimit(1)
    .layoutPriority(1)
}
```

<br /> 

### alignment

```
HStack(alignment: .center) {
  ...
  // 가운데 정렬선보다 위로 18포인트 아래
  Image("signbus")
    .alignmentGuide(VerticalAlignment.center, computeValue: { dimension in
      return dimension[VerticalAlignment.center] + 18
    })
}
```
<br />


### alignment enum

뷰의 중앙을 변경?

```
extension VerticalAlignment {
  enum BusAlignment: AlignmentID {
    static func defaultValue(in dimension: ViewDimensions) -> CGFloat {
      return dimension[VerticalAlignment.center]
    }
  }
  static let alignBus = VerticalAlignment(BusAlignment.self)
}

HStack(alignment: .alignBus) {
  ...
}
```

<br />

### grid
```
Grid(verticalSpacing: 5) {
  GridRow {
    Text("Hello World")
      .gridCellColumn(2)
  }
  GridRow {
    Image("phone")
    Image("house")
  }
}
```


<br />
<br />

## 🥑 실전

<br />
### 텍스트 띄워보기

```
import SwiftUI

struct ContentView: View {

  var body: some View {
    Text("Hello world")
      .font(.largeTitle)
      .foregroundColor(.green)
  }
}
```

<br />

### subView로 빼기 : 리액트처럼 컴포넌트 분리 개념

- 커맨트 + 클릭 => extrach subview

```
struct ContentView: View {
  let hikes: Hike.all()

  var body: some View {
    List(hikes, id: \.name) { hike in
      HikeCell(hike: hike)
    }
  }
}

// 📌 분리한 subview | 파일로 분리해도 된다
struct HikeCell: View {
  let hike: Hike

  HStack {
    Image(hike.imageUrl)
      .resizable()
      .aspectRatio(contentMode: .fit)
      .frame(width: 100, height: 100)
      .cornerRadius(20)
    VStack(alignment: .leading) {
      Text(hike.name)
      Text(String(format: "%.2f", hike.miles))
    }
  }
}
```

<br />

### NavigationView

전체를 씌운다

navigationTitle이랑 navigationBarTitleDisplayMode는 NavigationView {} 블록이 아니라 설정할 뷰 {} 블록 뒤에 위치

```
struct ContentView: View {
  //MARK: - properties
  let hikes = Hike.all()

  var body: some View {
    NavigationView {
      List(hikes, id: \.name) { hike in
        NavigationLink {
          HikeDetail(hike: hike)
        } label: {
          HikeListItem(hike: hike)
        }
      }

      .navigationTitle("Hikings")
      .navigationBarTitleDisplayMode(.inline)
    } 
  }
}
```

### List

```
let 어떤 데이터 = [["1", "2"], ["3", "4", "5"], ["ㅁㅇㄹㅁㅇㄹ", "ㅁㄴㅇ러ㅗㅁㄴㅇㄹ", "아ㅓㅗ니푸"]]

List(어떤 데이터, id: 데이터고유값) { 데이터 아이템 in
  ForEach(데이터 아이템, id: 데이터 아이템 고유값) { 데이터 아이템의 아이템 in 
    Text(데이터 아이템의 아이템.text)
  }
}
```

::::::::::::::::::::::::::::::결과::::::::::::::::::::::::::::::

![image](https://user-images.githubusercontent.com/86825214/210679366-23c9ecdd-0e81-43ca-bd3f-892a384a7ef6.png)

어떤 데이터가 배열 속의 배열이 있기 때문에 List안에 ForEach()로 배열 속 배열을 순환

<br />

### 배열 속 배열 아이템 리스트

Hstack으로 임베드해서 하나의 리스트안에 수평으로 텍스트를 그린다
```
let images = [["1", "2"], ["3", "4", "5"], ["ㅁㅇㄹㅁㅇㄹ", "ㅁㄴㅇ러ㅗㅁㄴㅇㄹ", "아ㅓㅗ니푸"]]

List(images, id: \.self) { image in
  HStack {
    ForEach(image, id: \.self) { item in
      Text(item)
    }
  }
}
```

<br />

### LazyVGrid

LazyVGrid의 columns인자는 \[GridItem] 이여야한다.

다양한 \[GridItem] 형태

- Array(repeating: GridItem(.flexible(), spacing: 5), count: 3) 
- \[GridItem(.fixed(100)), GridItem(.fixed(100)), GridItem(.fixed(100))]
- \[GridItem(.flexible(minimun: 10, maximun: 100)), GridItem(), GridItem(.fixed(50))]
- \[GridItem(.adaptive(minimun: 100, maximun: 120)), GridItem(.fixed(100)), GridItem(.fixed(100))]

```
let images = ["1", "2", "3", "4", "5", "ㅁㅇㄹㅁㅇㄹ", "ㅁㄴㅇ러ㅗㅁㄴㅇㄹ", "아ㅓㅗ니푸"]

let myColumns: [GridItem] = Array(repeating: GridItem(.flexible(), spacing: 10), count: 3)

LazyVGrid(columns: myColumns, spacing: 20) {
  ForEach(images, id: \.self) { image in
    Text(image)
  }
}
```
