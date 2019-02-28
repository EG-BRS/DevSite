
Layout
Xenas responsive layout is based on Bootstrap. If the browser supports CSS grid we will use that instead of Bootstraps grid system. You build your layout in rows and columns. Think “mobile first” when putting in your classes – always start with col-xs-12.

Panel
Indhold
Panel
Indhold
<div class="row">
    <div class="col-xs-12">
        <section class="panel panel-default">
            <header class="panel-heading">
                <h2 class="panel-title">Panel</h2>
            </header>
            <div class="panel-body">Indhold</div>
        </section>
    </div>
    <div class="col-xs-12">
        <section class="panel panel-default">
            <header class="panel-heading">
                <h2 class="panel-title">Panel</h2>
            </header>
            <div class="panel-body">Indhold</div>
        </section>
    </div>
</div>
By setting more classes you can tell how the layout should change based on how big the screen is.

(Adjust the browser size to see it in action)

Panel
Indhold
Panel
Indhold
<div class="row">
    <div class="col-xs-12 col-sm-6 col-md-7 col-lg-8 col-xl-9">
        <section class="panel panel-default">
            <header class="panel-heading">
                <h2 class="panel-title">Panel</h2>
            </header>
            <div class="panel-body">Indhold</div>
        </section>
    </div>
    <div class="col-xs-12 col-sm-6 col-md-5 col-lg-4 col-xl-3">
        <section class="panel panel-default">
            <header class="panel-heading">
                <h2 class="panel-title">Panel</h2>
            </header>
            <div class="panel-body">Indhold</div>
        </section>
    </div>
</div>
Classes
Extra Small

col-xs-1
col-xs-2
col-xs-3
col-xs-4
col-xs-5
col-xs-6
col-xs-7
col-xs-8
col-xs-9
col-xs-10
col-xs-11
col-xs-12
Small

col-sm-1
col-sm-2
col-sm-3
col-sm-4
col-sm-5
col-sm-6
col-sm-7
col-sm-8
col-sm-9
col-sm-10
col-sm-11
col-sm-12
Medium

col-md-1
col-md-2
col-md-3
col-md-4
col-md-5
col-md-6
col-md-7
col-md-8
col-md-9
col-md-10
col-md-11
col-md-12
Large

col-lg-1
col-lg-2
col-lg-3
col-lg-4
col-lg-5
col-lg-6
col-lg-7
col-lg-8
col-lg-9
col-lg-10
col-lg-11
col-lg-12
Extra Large

col-xl-1
col-xl-2
col-xl-3
col-xl-4
col-xl-5
col-xl-6
col-xl-7
col-xl-8
col-xl-9
col-xl-10
col-xl-11
col-xl-12