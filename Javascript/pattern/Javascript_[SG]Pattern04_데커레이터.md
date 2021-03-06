### JavaScript 데커레이터(decorator) 패턴

#### 데커레이터
```{.javascript}
호출 대상이 되는 객체에 추가 기능들을 자유롭게 추가하는 패턴

<body>
    <form id="personalInformation">
        <lable>First name:</lable>
        <input type="text" class="validate" data-validate-rules="required alphabet" name="firstName"><br/>
        <lable>Last name:</lable>
        <input type="text" class="validate" data-validate-rules="required alphabet" name="lastName"><br/>
        <lable>Age:</lable>
        <input type="text" class="validate" data-validate-rules="number" name="age"><br/>
        <lable>Gender:
            <select class="validate" data-validate-rules="required">
                <option>Male</option>
                <option>Female</option>
            </select>
        </lable><br/>
        <input type="submit"></input>
    </form>
    <script>
        (function () {
            var formPersonalInformation = document.getElementById("personalInformation"),
                validator = new Validator(formPersonalInformation);

            function Validator(form) {
                this.validatingForm = form;
                form.addEventListener("submit", function () {
                    if (!validator.validate(this)) {
                        event.preventDefault();
                        event.returnValue = false;
                        return false;
                    }
                    alert("Success to validate");
                    return true;
                });
            }
            Validator.prototype.ruleSet = {};
            Validator.prototype.decorate = function (ruleName, ruleFunction) {
                this.ruleSet[ruleName] = ruleFunction;
            }
            Validator.prototype.validate = function (form) {
                var validatingForm = form || this.validatingForm,
                    inputs = validatingForm.getElementsByClassName("validate"),
                    length = inputs.length,
                    i, j,
                    input,
                    checkRules,
                    rule,
                    ruleLength;
                for(i=0; i<length; i++) {
                    input = inputs[i];
                    if (input.dataset.validateRules) {
                        checkRules = input.dataset.validateRules.split(" ");
                        ruleLength = checkRules.length;
                        for (j=0; j<ruleLength; j++) {
                            rule = checkRules[j];
                            if (this.ruleSet.hasOwnProperty(rule)) {
                                if (!this.ruleSet[rule].call(null, input)) {
                                    return false;
                                }
                            }
                        }
                    }
                }
            };

            validator.decorate("required", function (input) {
                if (!input.value) {
                    input.focus();
                    alert(input.name + " is required");
                    return false;
                }
                return true;
            });
            validator.decorate("alphabet", function (input) {
                var regex = /^[a-zA-Z\s]*$/;
                if (!regex.test(input.value)) {
                    alert(input.name + " has to be only alphabets");
                    return false;
                }
                return true;
            });
            validator.decorate("number", function (input) {
                var regex = /^[0-9]*$/;
                if (!regex.test(input.value)) {
                    alert(input.name + " has to be only number");
                    return false;
                }
                return true;
            });
        }());
    </script>
</body>

Validator라는 클래스를 정의하여 prototype에 decorate()함수와 ruleset 변수를 추가해서 검증에
사용할 규칙을 곤리하고 추가할 수 있게 하고, 검증 규칙의 종류는 decorate() 함수를 통해 추가할 수 있다.

```