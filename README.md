# laravel-takamol

Laravel Takamol API Integration

# Installation

Begin by installing this package through Composer.

`composer require spacemudd/takamol`

If you're using Laravel 5.5+, this is all there is to do.

Should you still be on older versions of Laravel, the final steps for you are to add the
service provider of the package and alias the package. To do this, include them in your `config/app.php` file.

# DDD

This package is still at documentation stage and thus is empty. Once the docs are settled, I'll start on coding it out.

# Usage

Save a new `TCompany` object:

````
use Spacemudd\Takamol\TCompany;

$tCompany = TCompany::createFromLaborOfficeId(1000);
````

Save a new `TakamolEmployee` object:

````
$tEmployee = new TakamolEmployee();
$tEmployee->setNationalId(1000);
$tEmployee->references($anyModel);
$tEmployee->save();

$tEmployee->attach($tCompany);
````

Store activities related to the employee:

````
dispatch(new TakamolLoginEvent($tEmployee, $authClass));
dispatch(new TakamolLogoutEvent($tEmployee, $authClass));
dispatch(new TakamolAssignTaskEvent($tEmployee, $refClass));
dispatch(new TakamolCompletedTaskEvent($tEmployee, $refClass));
dispatch(new TakamolActivityLevelEvent($tEmployee, 37.00));
````

To export an Excel report:

````
use Spacemudd\Takamol\TCompany;

$company = TCompany::find(1000);

TakamolReport::setCompany($company)
  ->setPeriodFrom('2018-01-01')
  ->setPeriodTo('2018-01-29')
  ->download($reportName='takamol.csv');`
````




