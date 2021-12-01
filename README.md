# SQL-Quries

SELECT MI_Employer_Employee.Number, MI_Employer_Employee.fullname, MI_Employer_Employee.NicNumber, MI_Employer_Employee.FullName, MI_pRoll_ProcessInfo.Description, MI_pRoll_ProcessInfo.ProcessValue, 
                         MI_pRoll_ProcessInfo.PayPeriodCode, CONVERT(VARCHAR, MI_pRoll_PayPeriods.StartDate, 110) as StartDate, MI_eprf_hrDesignation.DesignationName, 
                         MI_eprf_hrOrgLevel2.Name AS Company,  MI_eprf_hrOrgLevel3.Name as dept, MI_eprf_hrOrgLevel4.Name AS Section,
                         MI_eprf_hrOrgLevel5.Name AS [Sub-Section], MI_pRoll_ProcessInfo.FormulaOrder, MONTH(MI_pRoll_PayPeriods.StartDate) AS Month, 
                         YEAR(MI_pRoll_PayPeriods.StartDate) AS Year, day(MI_pRoll_PayPeriods.StartDate) AS Date, Month(Getdate()) as CurrentMonth,
                          MI_eprf_hrLocation.LocationName, MI_Employer_Employee.DateOfAppointment, 
						  (select Count(*) from mi_ontime_attendance where EmployeeCode=89 and year(date)=2020 and month(date)=10  and present=1 ) as WorkingDays,
						  (select Count(*) from mi_ontime_attendance where EmployeeCode=89 and year(date)=2020 and month(date)=10  and expected=1 ) as workedDays,
						 CONVERT(VARCHAR, (select RequestDate from MI_DTS_EmployeeResignation where employeecode=804),110) resignDate, Month(resig.RequestDate) as ResignMonth,
                         MI_Employer_Employee.ConfirmedDate, MI_eprf_hrEmploymentType.ETypeName, MI_eprf_hrGrade.GradeName, salary.basicsalary, salary.grosssalary
FROM					 MI_pRoll_ProcessInfo  left outer join
						 MI_Employer_Employee on MI_pRoll_ProcessInfo.EmployeeCode=MI_Employer_Employee.employeecode  left outer join
						 MI_ONTIME_RptSelectedEmployee ON MI_pRoll_ProcessInfo.EmployeeCode = MI_ONTIME_RptSelectedEmployee.RptEmployeeCode  left outer join                        
                         MI_pRoll_PayPeriods ON MI_pRoll_ProcessInfo.PayPeriodCode = MI_pRoll_PayPeriods.PayPeriodCode  left outer join
                         MI_eprf_hrOrgLevel1 ON MI_Employer_Employee.level1code = MI_eprf_hrOrgLevel1.Level1Code  left outer join
                         MI_eprf_hrOrgLevel3 ON MI_Employer_Employee.level3code = MI_eprf_hrOrgLevel3.Level3Code  left outer join
						 MI_eprf_hrOrgLevel5 ON MI_Employer_Employee.level5code = MI_eprf_hrOrgLevel5.Level5Code  left outer join
						 MI_eprf_hrOrgLevel2 ON MI_Employer_Employee.level2code = MI_eprf_hrOrgLevel2.Level2Code  left outer join
						 MI_eprf_hrDesignation ON MI_Employer_Employee.DesignationCode = MI_eprf_hrDesignation.DesignationCode  left outer join
                         MI_eprf_hrJobCategory ON MI_Employer_Employee.CategoryCode = MI_eprf_hrJobCategory.JobCategoryCode  left outer join
                         MI_eprf_hrEmploymentType ON MI_Employer_Employee.EmploymentTypeCode = MI_eprf_hrEmploymentType.ETypeCode  left outer join
                         MI_eprf_hrGrade ON MI_Employer_Employee.GradeCode = MI_eprf_hrGrade.GradeCode  left outer join
                         MI_eprf_hrOrgLevel3 AS MI_eprf_hrOrgLevel3_1 ON MI_Employer_Employee.Level3Code = MI_eprf_hrOrgLevel3_1.Level3Code LEFT OUTER JOIN
                         MI_eprf_hrLocation ON MI_Employer_Employee.LocationCode = MI_eprf_hrLocation.LocationCode LEFT OUTER JOIN
                         MI_eprf_hrOrgLevel4 ON MI_Employer_Employee.level4code = MI_eprf_hrOrgLevel4.Level4Code  LEFT OUTER JOIN
						 MI_DTS_EmployeeResignation resig on resig.EmployeeCode=MI_Employer_Employee.employeecode left outer join
						 MI_DTS_EmployeeSalaryDetail_PAK salary on salary.EmployeeCode=MI_Employer_Employee.EmployeeCode left outer join
						 mi_ontime_attendance att on att.EmployeeCode=MI_Employer_Employee.employeecode


						 WHERE  (MONTH(MI_pRoll_PayPeriods.StartDate) = 11) AND (YEAR(MI_pRoll_PayPeriods.StartDate) = 2020) AND  MI_pRoll_ProcessInfo.processvalue!=0 and
						  
						  MI_pRoll_ProcessInfo.EmployeeCode=804
						 --and MI_pRoll_PayPeriods.PayPeriodCode=959
select * from MI_RPT_Report where ReportTitle in ('Employees without Goals', 'Employee Goal Summary', 'Appraisee List Assigned to an Evaluation', 'PMS Progress Report', 'Performance Summary', 'Goal Summary 2', 'Culture Values Report', 'Competencies Report', 'Development Plan Report', 
'Additional Accomplishments Report', 'Potential Assesement Report', 'PMS Sign-Off Staus Report', 'Trait Scores Report', 'Final Performance Summary', 'Goal Summary', 'Submission Status of Goals', 'Employees Assigned Performance Report')

====================

SELECT        MI_Employer_Employee.Number, MI_Employer_Employee.fullname, MI_Employer_Employee.NicNumber, MI_Employer_Employee.FullName, MI_pRoll_ProcessInfo.Description, MI_pRoll_ProcessInfo.ProcessValue, 
                         MI_pRoll_ProcessInfo.PayPeriodCode, CONVERT(VARCHAR, MI_pRoll_PayPeriods.StartDate, 110) as StartDate, MI_eprf_hrDesignation.DesignationName, 
                         MI_eprf_hrOrgLevel2.Name AS Company,  MI_eprf_hrOrgLevel3.Name as dept, MI_eprf_hrOrgLevel4.Name AS Section,
                         MI_eprf_hrOrgLevel5.Name AS [Sub-Section], MI_pRoll_ProcessInfo.FormulaOrder, MONTH(MI_pRoll_PayPeriods.StartDate) AS Month, 
                         YEAR(MI_pRoll_PayPeriods.StartDate) AS Year, day(MI_pRoll_PayPeriods.StartDate) AS Date, Month(Getdate()) as CurrentMonth,
                          MI_eprf_hrLocation.LocationName, MI_Employer_Employee.DateOfAppointment, 
						  (select Count(*) from mi_ontime_attendance where EmployeeCode=89 and year(date)=2020 and month(date)=10  and present=1 ) as WorkingDays,
						  (select Count(*) from mi_ontime_attendance where EmployeeCode=89 and year(date)=2020 and month(date)=10  and expected=1 ) as workedDays,
						 CONVERT(VARCHAR, (select RequestDate from MI_DTS_EmployeeResignation where employeecode=804),110) resignDate, Month(resig.RequestDate) as ResignMonth,
                         MI_Employer_Employee.ConfirmedDate, MI_eprf_hrEmploymentType.ETypeName, MI_eprf_hrGrade.GradeName, salary.basicsalary, salary.grosssalary
FROM					 MI_pRoll_ProcessInfo  left outer join
						 MI_Employer_Employee on MI_pRoll_ProcessInfo.EmployeeCode=MI_Employer_Employee.employeecode  left outer join
						 MI_ONTIME_RptSelectedEmployee ON MI_pRoll_ProcessInfo.EmployeeCode = MI_ONTIME_RptSelectedEmployee.RptEmployeeCode  left outer join                        
                         MI_pRoll_PayPeriods ON MI_pRoll_ProcessInfo.PayPeriodCode = MI_pRoll_PayPeriods.PayPeriodCode  left outer join
                         MI_eprf_hrOrgLevel1 ON MI_Employer_Employee.level1code = MI_eprf_hrOrgLevel1.Level1Code  left outer join
                         MI_eprf_hrOrgLevel3 ON MI_Employer_Employee.level3code = MI_eprf_hrOrgLevel3.Level3Code  left outer join
						 MI_eprf_hrOrgLevel5 ON MI_Employer_Employee.level5code = MI_eprf_hrOrgLevel5.Level5Code  left outer join
						 MI_eprf_hrOrgLevel2 ON MI_Employer_Employee.level2code = MI_eprf_hrOrgLevel2.Level2Code  left outer join
						 MI_eprf_hrDesignation ON MI_Employer_Employee.DesignationCode = MI_eprf_hrDesignation.DesignationCode  left outer join
                         MI_eprf_hrJobCategory ON MI_Employer_Employee.CategoryCode = MI_eprf_hrJobCategory.JobCategoryCode  left outer join
                         MI_eprf_hrEmploymentType ON MI_Employer_Employee.EmploymentTypeCode = MI_eprf_hrEmploymentType.ETypeCode  left outer join
                         MI_eprf_hrGrade ON MI_Employer_Employee.GradeCode = MI_eprf_hrGrade.GradeCode  left outer join
                         MI_eprf_hrOrgLevel3 AS MI_eprf_hrOrgLevel3_1 ON MI_Employer_Employee.Level3Code = MI_eprf_hrOrgLevel3_1.Level3Code LEFT OUTER JOIN
                         MI_eprf_hrLocation ON MI_Employer_Employee.LocationCode = MI_eprf_hrLocation.LocationCode LEFT OUTER JOIN
                         MI_eprf_hrOrgLevel4 ON MI_Employer_Employee.level4code = MI_eprf_hrOrgLevel4.Level4Code  LEFT OUTER JOIN
						 MI_DTS_EmployeeResignation resig on resig.EmployeeCode=MI_Employer_Employee.employeecode left outer join
						 MI_DTS_EmployeeSalaryDetail_PAK salary on salary.EmployeeCode=MI_Employer_Employee.EmployeeCode left outer join
						 mi_ontime_attendance att on att.EmployeeCode=MI_Employer_Employee.employeecode


						 WHERE  (MONTH(MI_pRoll_PayPeriods.StartDate) = 11) AND (YEAR(MI_pRoll_PayPeriods.StartDate) = 2020) AND  MI_pRoll_ProcessInfo.processvalue!=0 and
						  
						  MI_pRoll_ProcessInfo.EmployeeCode=804
						 --and MI_pRoll_PayPeriods.PayPeriodCode=959
             
             
   =======================
    select * from MI_DTS_EmployeeSalaryDetail_PAK where EmployeeCode=89 

select * from MI_DTS_EmployeeResignation where employeecode=89
select * from MI_pRoll_ProcessInfo where EmployeeCode=89 
select * from MI_Ontime_attendance where employeecode=804 and MONTH(date)=11 order by Date desc
select * from MI_DTS_EmployeeTransactionDetail_PAK where EmployeeCode=89

(select Count(*) from mi_ontime_attendance where EmployeeCode=89 and year(date)=2020 and month(date)=10  and present=1 ) as PresentDays
order by Date desc
    
