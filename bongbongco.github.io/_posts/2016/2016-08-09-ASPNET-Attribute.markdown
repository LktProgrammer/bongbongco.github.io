---
layout: post
title: ASP.NET 대괄호 (어트리뷰트).
categories: [Development]
tags: [ASP.NET, Attribute]
fullview: false
comments: true
published: true
---

대괄호로 되어있는 부분은 어트리뷰트(Attribute)라고 합니다.  

꼭 메서드에만 사용되는 것은 아니고, 클래스나 프로퍼티등의 항목에도 붙일 수 있는데요.   어트리뷰트를 붙이는 대상에 특정 속성을 부여하려고 할 때 사용합니다.  

~~~
[TestMethod]
public void ProductListTest()
{
    ProductsController controller = new ProductsController();
    ViewResult result = (ViewResult)controller.List();
 
    List<Products> products = (List<Products>)result.ViewData.Model;
    Assert.AreEqual(3, products[2].ProductID);
}
~~~

위 예제 코드에서 TestMethod 어트리뷰트를 ProductListTest메서드에 붙임으로써, 이 메서드가 유닛 테스트 메서드임을 표시하는 것이죠. 이렇게 표시된 메서드는 Visual Studio가 테스트 메서드로 인식을 하게 됩니다.  

비슷한 예로 [WebMethod]가 있는데요,  

~~~
[WebMethod]
public string HelloWorld()
{
    return "Hello World";
}
~~~

위 예제에서 HelloWorld메서드는 웹 서비스를 통해서 외부에 노출될 수 있게 됩니다.  
그리고 필요한 경우에는 직접 이런 어트리뷰트를 만들어서 사용할 수도 있습니다.  

[MSDN 참고](https://social.msdn.microsoft.com/Forums/ko-KR/00a2a98b-2b5f-4520-85a5-d44a82cdf443/-?forum=visualcsharpko)  
