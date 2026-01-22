# Active Context

## Current Focus
إنشاء Memory Bank للمشروع وتوثيق البنية والمعلومات الأساسية.

## Recent Changes
- المشروع هو fork من repository principal لـ Cline
- تم إنشاء .clinerules/ في المستويين العام والعمل

## Next Steps
- إكمال إنشاء ملفات Memory Bank المتبقية
- توثيق الأنماط والتقنيات المهمة
- فهم بنية الكود بشكل أعمق للتطوير المستقبلي

## Active Considerations
- فهم كيفية عمل نظام الـ gRPC-like communication
- دراسة كيفية إدارة الحالة بين الـ extension والـ webview
- فهم نظام الأدوات وتنفيذها

## Important Patterns & Preferences
- استخدام fetch proxy-aware من `@/shared/net` للاتصالات الشبكية
- تعريفات الـ proto في `proto/` directory
- توليد الأنواع عبر `npm run protos`
- اتباع أنماط الـ .clinerules للممارسات الخاصة بالمشروع

## Learnings & Insights
- المشروع يستخدم TypeScript في extension و Go في CLI
- Communication بين webview و extension عبر message passing
- دعم كبير لمزودين متعددين للـ AI
- MCP integration للـ extensibility
