<!DOCTYPE html>
<html ng-app="myApp">
<head>
<script src="angular.min.js"></script>
</head>
<body>
<div ng-controller="menucontroller">
      <h2>Order Menu</h2>
    <table class="table">
        <tr>
            
            <th>Item</th>
            <th>Cost</th>
            <th>Add to cart</th>
            <th></th>
        </tr>
        <tr ng-repeat="item in lst">
            
            <td>{{item.name}}</td>
            <td>{{item.price}}</td>
            <td></td>
            <td><button ng-click="addtocart(item)">+</button></td>
        </tr>
        <tr>
            
        </tr>
    </table>

    
    
    
</div>

<div ng-controller="ordercontroller">

Total:{{total}}
 
</div>
    

<script>
angular.module('myApp', [])
.service("menuserve",function(){
this.items=function(){
var products=[
{name:"veg. briyani",price:120},
{name:"noodles",price:150},
{name:"fried rice",price:100}
];
return products;
}
})
.service("orderserve",function(){
this.orderitems=[];

this.addtocart=function(item){
    this.orderitems.push(item);
}

this.total=function(){
var tot=0;
this.orderitems.forEach(function(item){
   tot +=item.price;

});
return tot;
}

})
.controller('menucontroller', function($scope,$rootScope,menuserve,orderserve){
$scope.lst=menuserve.items();

$scope.addtocart=function(item){
       orderserve.addtocart(item);
       $rootScope.total=orderserve.total();
}

})
.controller('ordercontroller', function($scope,menuserve,orderserve){
$scope.lst1=orderserve.orderitems;
});    
</script>
<br>
</body>
</html>
