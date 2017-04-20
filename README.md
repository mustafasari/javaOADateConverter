Microsoft's OLE Automation Date Converter for Java
# How to convert Java Date to OADate:

        /**
        * Convert Date to Microsoft OLE Automation - OADate type
        * @param date
        * @return
        * @throws ParseException
        */
        public static String convertToOADate(Date date) throws ParseException {
        double oaDate;
        SimpleDateFormat myFormat = new SimpleDateFormat("dd MM yyyy");
        Date baseDate = myFormat.parse("30 12 1899");
        Long days = TimeUnit.DAYS.convert(date.getTime() - baseDate.getTime(), TimeUnit.MILLISECONDS);

        oaDate = (double) days + ((double) date.getHours() / 24) + ((double) date.getMinutes() / (60 * 24)) + ((double)                     date.getSeconds() / (60 * 24 * 60));
        return String.valueOf(oaDate);
        }
# How to convert OADate to Java Date:

    /**
     * Convert Microsoft un OLE Automation - OADate to Java Date.
     * @param date
     * @return
     * @throws ParseException
     */
    public static Date convertFromOADate(double d) throws ParseException {
        double  mantissa = d - (long) d;
        double hour = mantissa*24;
        double min =(hour - (long)hour) * 60;
        double sec=(min- (long)min) * 60;


        SimpleDateFormat myFormat = new SimpleDateFormat("dd MM yyyy");
        Date baseDate = myFormat.parse("30 12 1899");
        Calendar c = Calendar.getInstance();
        c.setTime(baseDate);
        c.add(Calendar.DATE,(int)d);
        c.add(Calendar.HOUR,(int)hour);
        c.add(Calendar.MINUTE,(int)min);
        c.add(Calendar.SECOND,(int)sec);

        return c.getTime();
    }
