def calculate_postpaid_bill(monthly_fee, total_minutes, total_gb, days_passed, total_days=30):
    # حساب المبلغ المستحق بالتناسب
    due_amount = (monthly_fee / total_days) * days_passed
    
    # حساب الدقائق المتناسبة مع الأيام
    allocated_minutes = (total_minutes / total_days) * days_passed
    
    # حساب الغيغابايتات المتناسبة مع الأيام
    allocated_gb = (total_gb / total_days) * days_passed
    
    print(f"--- تفاصيل الفاتورة لغاية اليوم ({days_passed} من {total_days} يوم) ---")
    print(f"المبلغ المستحق: {round(due_amount, 2):,} دينار عراقي")
    print(f"الدقائق المتاحة: {round(allocated_minutes, 1)} دقيقة (من أصل {total_minutes})")
    print(f"الإنترنت المتاح: {round(allocated_gb, 2)} غيغابايت (من أصل {total_gb} GB)")

# مثال على خطك (اشتراك 25 ألف، 500 دقيقة، 12 غيغابايت، ومرور 24 يوم)
calculate_postpaid_bill(
    monthly_fee=25000, 
    total_minutes=500, 
    total_gb=12, 
    days_passed=24
)
