
<!DOCTYPE html>

<html lang="en" >

<head>
    <?php echo $header_content; ?>
    <style>
        #p_e989_0 {
            padding-left: 10px;
            background-color: lightgray;
            padding: 2px;
            margin-top: 5px;
            margin-bottom: 5px;
        }

        #span_e989_0 {
            background-color: #97cc59;
            height: 100%;
            width: 100%;
            padding: 2px;
            margin-left: 20px;
            padding-left: 6px;
        }

        #b_e989_0 {
            color: white;
        }

        #span_e989_1 {
            font-weight: bold;
            padding-left: 5px;
        }
    </style>
</head>


<body class="page-header-fixed page-sidebar-closed-hide-logo page-md" ng-app="routerApp">
    <!-- BEGIN CONTAINER -->
    <div class="wrapper">
        <!-- BEGIN HEADER -->
        <?php echo $navigationmenu_content ?>
        <!-- END HEADER -->
    

                <div class="col-md-4" style="height:400px;margin-top:15px">
                    <div style="border: 1px solid lightgrey;border-bottom-left-radius: 2em;border-bottom-right-radius:2em;height: 100%;">
                        <img style="max-height:100%;max-width:100%;" src="../../App/assets/Dashboard/data-gathering-icon-block-2.png" />

                        <p id="p_e989_0" style="margin-top:13px">
                            <span id="span_e989_0">
                                <b id="b_e989_0">0</b>
                            </span>
                            <span id="span_e989_1">Readings</span>
                        </p>

                    </div>

                </div>

                <style>

                    vic-input-css i:hover {
                        color: cornflowerblue;
                    }

                    vic-input-css {
                        display: inline-block;
                        width: 30px;
                        position: absolute;
                    }

                    vic-input-css i {
                        color: #ccc;
                        display: block;
                        position: absolute;
                        /* margin: -11px 2px 4px 10px; */
                        z-index: 3;
                        width: 16px;
                        font-size: 13px;
                        text-align: center;
                        top: 3%;
                        left: 65%;
                        cursor: pointer;
                    }
                    vic-input-css input {
                        border: 0 !important;
                        border-bottom: 1px solid #bfbfbf !important;
                        box-shadow: none;
                        padding-right: 38% !important;
                        padding-left: 10% !important;
                        text-align: center;
                    }
                        vic-input-css .vic-field-info-container {
                            background-color: white;
                            width: 185px;
                            padding: 5px;
                        }
                </style>

                <script type="text/javascript">

                    routerApp.controller("testController", function ($scope) {
              
                        $scope.FancyModel = "test";
                        $scope.lastUpdated = "2wks";
                        $scope.UpdateHistory = function () {
                            $scope.lastUpdated = "testttt";
                        }

                    });

       

                    routerApp.directive('vicInput', function ($http, $compile, $parse) {
                        return {         
                            link: function (scope, element, attr) {
                              
                                var templateString = '<vic-input-css style="width:100px">' +
                                                     '<input type="text" ng-model="[placeholder]" class="form-control" placeholder="null" />' +
    '<i popover-placement="right" ng-click="TogglePopover()" ng-style="hidePopover === true ? { \'background-color\':\'red\' } : { \'background-color\':\'red\' }" >{{ [lastUpdate] }} </i>' +

                                                     '<div class="vic-field-info-container" ng-hide="hidePopover" style="left: [left];top: [top];border: 1px solid black;">' +
                                                        '<div class="vic-field-info-header">' +
                                                            '<h5 class="vic-field-info-title" style="font-size: 0.8em">Last updated: 12:12:32 02-04-2017</h5>' +
                                                            '<h5 class="vic-field-info-title" style="font-size: 0.8em">Value: 23<h5>' +
                                                            '<button class="btn" style="width:60%" ng-click="GetAllModifications()">Show History</button>' +
                                                            '<button class="btn" style="width:40%" ng-click="TogglePopover()">Close</button>' +
                                                        '</div>' +
                                                        '<div class="vic-field-info-content" style="max-height: 90px;overflow-x:hidden;overflow-y:auto;margin-top:8px" >' +
                                                          '<ul style="list-style: none;margin-top:5px;margin-left: -31px;">' +
                                                            '<li style="font-size:0.7em" ng-repeat="modification in Modifications">{{ $index }}) {{ modification.date }} value: {{ modification.value }}</li>' +
                                                          '</ul>' +

                                                        '</div>' +
                                                     '</div>' +
                                                  '</vic-input-css>';

                                
                                var inputPopoverWidth = element.attr('popover-width-s');

                                templateString = templateString.replace("[lastUpdate]", "lastUpdated");

                                switch (inputPopoverWidth) {
                                    case 1:
                                        templateString = templateString.replace("[left]", "90px");
                                        templateString = templateString.replace("[top]", "-40px");
                                    default:
                                }

                                var $template = $(templateString);

                                var newScope = scope.$new();

                                newScope.Modifications = [];

                                newScope.hidePopover = true;

                                newScope.TogglePopover = function (event) {
                                    newScope.hidePopover = !newScope.hidePopover;
                                }

                                newScope.GetAllModifications = function () {
                                    newScope.Modifications.push({ date: "12:12:32 02-04-2017", value: "23" });
                                    newScope.Modifications.push({ date: "12:12:32 02-04-2017", value: "23" });
                                    newScope.Modifications.push({ date: "12:12:32 02-04-2017", value: "23" });
                                    newScope.Modifications.push({ date: "12:12:32 02-04-2017", value: "23" });
                                }

                                var inputVictModel = element.attr('vict-model-s');
                                

                                $template.find('input').attr('ng-model', inputVictModel);

                               

                                element.replaceWith($compile($template.prop('outerHTML'))(newScope));
                            }
                        }
                    });


                </script>

                <div class="col-md-4" style="margin-top:10px" ng-controller="testController">
                    <button ng-click="UpdateHistory()">updated</button>
                    <vic-input vict-model-s="FancyModel" popover-widt-s="1" ></vic-input>
                   
                </div>

            </div>
          
        </div>


    </div>

</body>

</html>
