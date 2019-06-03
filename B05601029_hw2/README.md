# **作業二**
黃哲全 B05601029

---



*Pagination from bootstrap*

```
<!-- 分頁 -->
    <div class="row" id="page">
        <div class="col">
            <nav aria-label="Page navigation example">
                <ul id="page-number" class="pagination justify-content-center">
                    <li class="page-item active"><a class="page-link" href="#">1</a></li>
                    <li class="page-item"><a class="page-link" href="#">2</a></li>
                    <li class="page-item"><a class="page-link" href="#">3</a></li>
                </ul>
            </nav>
        </div>
    </div>
```
*Contact info in footer, everything in center*
```
<div id="contact" class="offset">
        <footer class="row justify-content-center">
            <div class="col-md-5 text-center">
                <strong>Contact Info</strong>
                <br>
                <p>+886966135759 <br>alvinwijaya2798@gmail.com</p>
                <a href="https://www.google.com" class="fa fa-facebook"></a>
                <a href="https://www.facebook.com/alvin.wijaya.3367" class="fa fa-google"></a>
                <a href="https://www.instagram.com/alvinnnw/" class="fa fa-instagram"></a>
            </div>
    </div>
    </footer>
```
*A responsive navbar, following the section I'm in*
```
<body data-spy="scroll" data-target="#navbarResponsive">

    <div id="home">
        <nav class="navbar navbar-expand-md navbar-dark bg-dark fixed-top">
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarResponsive">
                    <span class="navbar-toggler-icon"></span>
    </button>
            <div class="collapse navbar-collapse" id="navbarResponsive">
                <ul class="navbar-nav ml-auto">
                    <li class="nav-item">
                        <a class="nav-link" href="#home">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#aboutme">About Me</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#product">Product</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#contact">Contact</a>
                    </li>

                </ul>
            </div>
        </nav>
```
*A Home icon in top right to redirect to home where all info belongs*
```
<nav class="navbar navbar-expand-md navbar-dark bg-dark fixed-top">
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarResponsive">
                        <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarResponsive">
            <ul class="navbar-nav ml-auto">
                <li class="nav-item">
                    <a class="nav-link" href="./index.html">Home</a>
                </li>

            </ul>
        </div>
    </nav>
    </nav>
```
*A structure of 新增資料 I get much of it from teacher's code*
```
<div class="row">
            <div class="col">
                <div class="form-group row">
                    <label for="inputProductName" class="col-sm-2 col-form-label">商品名稱
                        <br>Input Product Name
                    </label>
                    <div class="col-sm-10">
                        <input type="text" class="form-control" id="inputProductName" placeholder="請輸入商品名稱" value="米家自動感應洗手機">
                    </div>
                </div>

                <div class="form-group row">
                    <label for="inputProductPrice" class="col-sm-2 col-form-label">商品價格
                        <br>Input Product Price
                    </label>
                    <div class="col-sm-10">
                        <input type="number" class="form-control" id="inputProductPrice" placeholder="請輸入商品價格" value="395">
                    </div>
                </div>

                <div class="form-group row">
                    <label for="inputProductCount" class="col-sm-2 col-form-label">商品數量<br>Input Product Amount </label>
                    <div class="col-sm-10">
                        <input type="number" class="form-control" id="inputProductCount" placeholder="請輸入商品數量" value="10">
                    </div>
                </div>

                <div class="form-group row">
                    <label for="inputProductImage" class="col-sm-2 col-form-label">圖片網址
                        <br>Input Product Image Link
                    </label>
                    <div class="col-sm-10">
                        <input type="text" class="form-control" id="inputProductImage" placeholder="請輸入商品圖片網址" value="https://i01.appmifile.com/v1/MI_18455B3E4DA706226CF7535A58E875F0267/pms_1542426682.20729915.png">
                    </div>
                </div>

                <!-- 工具列 -->
                <div class="form-group row">
                    <div class="col">
                        <button id="insertfile" type="button" class="btn btn-primary">新增</button>
                    </div>
                </div>
            </div>
        </div>
```
*插入分頁數字, i change attribute to product list for after i click on order page number it still shows the product, not get back to the top*
```

        for (var i = 1; i <= pageNum; i++) {
            $a = $('<a>').attr('class', 'page-link').attr('href', '#product-list').text(i)

            $a.on('click', function() {
                var i = $(this).text()
                showItems(Number(i))
            })

            var strActive = ((i == 1) ? ' active' : '')

            $li = $('<li>').attr('class', 'page-item' + strActive).append($a)
            $('#page-number').append($li)
        }
```
*清空 product-list and to hide the page number before tapping into search*
```
    $('#product-list').empty();
    $('#page').hide()

    var items = null
    var pageCount = 16
    var showItems = (page) => {
        if (items == null) return
        var start = (page - 1) * pageCount
        var end = start + pageCount - 1
        $('#product-list').empty();
        for (var i = start; i <= end; i++) {
            newItem(items[i])
        }
    }

    var newItem = (item) => {
        $img = $('<img>').attr('class', 'image').attr('src', item.image)
        $h3 = $('<h3>').attr('class', 'name').text(item.name)
        $p = $('<p>').attr('class', 'price').text('NT$ ' + item.price)

        $item = $('<div>').attr('class', 'item').append($img).append($h3).append($p)
        $col = $('<div>').attr('class', 'col-*').append($item)

        $('#product-list').append($col)
    }


    var newPage = (n) => {
        var pageNum = n / 16
        pageNum = (n % 16 != 0) ? pageNum + 1 : pageNum

        $('#page-number').empty()
```
A jumbotron with product button which leads to product section.
```
<div id="aboutme" class="offset">
            <div class="jumbotron">
                <div class="row">
                    <div class="col-12">
                        <h3 class="heading">About Me</h3>
                        <div class="heading-underline"></div>
                    </div>
                    <div class="padding" style='width:100%;'>
                        <div class="container">
                            <div class="row" style='justify-content:center;'>
                                <div class="col-md-6 image-col ">
                                    <img src="img/me.JPG">
                                </div>
                                <div class="col-md-6 text-center introduction-div">
                                    <div>
                                        <h2>Introduction</h2>
                                        <p class="lead">I am Alvin, a sales and web developer for XiaoMixx</p>
                                        <a class="btn btn-primary btn-lg" href="#product">Product</a>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
```