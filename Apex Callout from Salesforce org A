public class salesforceOrgB {
    private Static final string endpoint_url = 'callout:connectSFDC_A/services/apexrest/Cases/';
    // get case status from org B
    @AuraEnabled(Cacheable = true)   
	public static Map<object,Integer> getCaseRecords()
    {
        
        List<object> statusofCase =  new List<object> ();
        Http h = new Http();
        HttpRequest request = new HttpRequest();
        request.setEndpoint(endpoint_url);
        request.setMethod('GET');
        HttpResponse response= new HttpResponse();
        response=h.send(request);
        List<Object> caseList =  (List<Object>)JSON.deserializeUntyped(response.getBody());
        system.debug(caseList.size());
        for(Object obj: caseList)
        {
            Map<string,Object> caseMapping = (Map<string,Object>)obj;
            statusofCase.add(caseMapping.get('Status'));
        }
       
        Map<object,Integer> CaseCount = new Map<object,Integer>();

        for(Object key : statusofCase)
        {
            if(!CaseCount.containsKey(key)){
            CaseCount.put(key,0);
            }
            Integer currentInt=CaseCount.get(key)+1;
            CaseCount.put(key,currentInt);
        }
        system.debug(CaseCount.values());
        return CaseCount;
    }
	
    // create case record on org B
	@AuraEnabled(Cacheable = true)    
    public static String createCaseRecord(string sub, string stat, string org, string prior)
    {
        Http h = new Http();
        HttpRequest request = new HttpRequest();
        request.setEndpoint(endpoint_url);
        request.setMethod('POST');
        request.setHeader('Content-Type', 'application/json;charset=UTF-8');
        request.setBody('{"subject": "'+sub+'","status": "'+stat+'", "origin": "'+org+'", "priority": "'+prior+'"}');
        HttpResponse response = new HttpResponse();
        response = h.send(request);
        system.debug(response.getBody());
        return response.getBody();
    }
}
