# yii2-Customized-Query-with-Pagination
yii2 Customized Query with Pagination


##Problem: When I customized the query like range fields, the post method(form/ajax) need transfer params to the Global Get to make pagination working.


##My Demo Codes of the Controller
```
if (!empty(Yii::$app->request->post())){
$result_from = Yii::$app->request->post('DemoCollectionSearch')['result_from'];
$result_to = Yii::$app->request->post('DemoCollectionSearch')['result_to'];
}else{
$result_from = Yii::$app->request->get('result_from');
$result_to = Yii::$app->request->get('result_to');
}

$searchModel = new DemoCollectionSearch();

$searchModel->result_from = $result_from;
$searchModel->result_to = $result_to;




$_GET += array(
'result_from' => $dresult_from,
'result_to' => $result_to,
); // define


```



###Original Article link of YII 1.1
http://www.yiiframework.com/forum/index.php/topic/3214-yii%E6%9F%A5%E8%AF%A2%E6%9D%A1%E4%BB%B6%E5%88%86%E9%A1%B5%E7%9A%84%E9%97%AE%E9%A2%98/

不管怎样，你需要一种能持久化数据的方式。你可以有以下几种选择：
1. GET参数
2. SESSION
3. COOKIE
4. hidden field

我的建议是尽量用GET参数，尤其是这种搜索查询页面。 

在action中得到post数据后写入$_GET就行了
```
$form=new SearchForm;
if(isset($_POST['SearchForm']))
{
    $form->attributes=$_POST['SearchForm'];
    $_GET['keyword'] = $form->keyword;
    $_GET['cat_id'] = $form->cat_id;
} elseif(isset($_GET['keyword'])) {
    if(isset($_GET['keyword'])) $form->keyword=$_GET['keyword'];
    if(isset($_GET['cat_id'])) $form->cat_id=$_GET['cat_id'];
} else {
既没post也没get数据的话，设定默认查询条件
}
if($form->validate())
{
....处理查询
｝



```
