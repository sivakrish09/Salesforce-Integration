@RestResource(urlMapping='/Cases/*')
Global class salesforceOrgAIntegrate {
    @HttpGet
    Global Static List<Case>  getcaseRecord()
    {
       
        List<Case> resultList =  [SELECT Id,CaseNumber,Subject,Status,Origin,Priority
                        FROM Case ];
       return resultList;
    }
    @HttpPost
    Global static string createCase(String subject, String status,
        String origin, String priority)
    {
		Case c = new Case();
		c.Subject = subject;
		c.Status = status;
		c.Origin = origin;
		c.Priority = priority;
		insert c;
        system.debug(c.Id);
		return c.ID;       
    }

}
