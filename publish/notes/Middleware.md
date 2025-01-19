interrupts every request from a web page

steps:
1. make middleware file using `php artisan make:middleware`
2. add logic in `handle()` function in middle ware file utilizing the `request` 
3. register in the `kernel.php`
4. add middleware to route either one by one or using group