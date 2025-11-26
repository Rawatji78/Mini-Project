import React, { useState, useEffect } from 'react';
import { Menu, X, ChevronRight, TrendingUp, Users, Zap, Shield, ArrowRight, Star } from 'lucide-react';
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer, BarChart, Bar } from 'recharts';

export default function BusinessWebsite() {
  const [menuOpen, setMenuOpen] = useState(false);
  const [scrolled, setScrolled] = useState(false);
  const [activeTab, setActiveTab] = useState('analytics');

  useEffect(() => {
    const handleScroll = () => setScrolled(window.scrollY > 50);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const chartData = [
    { month: 'Jan', revenue: 4000, users: 2400 },
    { month: 'Feb', revenue: 3000, users: 1398 },
    { month: 'Mar', revenue: 2000, users: 9800 },
    { month: 'Apr', revenue: 2780, users: 3908 },
    { month: 'May', revenue: 1890, users: 4800 },
    { month: 'Jun', revenue: 2390, users: 3800 },
  ];

  const performanceData = [
    { name: 'Performance', value: 85 },
    { name: 'Security', value: 92 },
    { name: 'UX/UI', value: 78 },
    { name: 'Support', value: 88 },
  ];

  const features = [
    { icon: TrendingUp, title: 'Real-time Analytics', desc: 'Track metrics and insights instantly' },
    { icon: Users, title: 'Team Collaboration', desc: 'Work together seamlessly' },
    { icon: Zap, title: 'Lightning Fast', desc: 'Optimized performance' },
    { icon: Shield, title: 'Enterprise Security', desc: 'Bank-level protection' },
  ];

  const testimonials = [
    { name: 'Sarah Johnson', role: 'CEO at TechCorp', text: 'Transformed our business operations completely.' },
    { name: 'Mike Chen', role: 'COO at StartupX', text: 'Best platform weve integrated with our stack.' },
    { name: 'Emma Wilson', role: 'CTO at InnovateLabs', text: 'Exceptional support and feature set.' },
  ];

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900 text-white overflow-hidden">
      {/* Navigation */}
      <nav className={`fixed w-full top-0 z-50 transition-all duration-300 ${scrolled ? 'bg-slate-900/95 backdrop-blur shadow-lg' : 'bg-transparent'}`}>
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex justify-between items-center h-16">
            <div className="flex items-center space-x-2">
              <div className="w-10 h-10 bg-gradient-to-r from-blue-400 to-purple-600 rounded-lg flex items-center justify-center font-bold">B</div>
              <span className="text-xl font-bold">BusinessHub</span>
            </div>
            
            <div className="hidden md:flex space-x-8">
              {['Features', 'Pricing', 'Analytics', 'Testimonials'].map(item => (
                <a key={item} href="#" className="hover:text-blue-400 transition">
                  {item}
                </a>
              ))}
            </div>

            <div className="hidden md:flex space-x-4">
              <button className="px-4 py-2 text-blue-400 hover:text-blue-300">Sign In</button>
              <button className="px-6 py-2 bg-gradient-to-r from-blue-500 to-purple-600 rounded-lg hover:shadow-lg hover:shadow-blue-500/50 transition">
                Get Started
              </button>
            </div>

            <button onClick={() => setMenuOpen(!menuOpen)} className="md:hidden">
              {menuOpen ? <X size={24} /> : <Menu size={24} />}
            </button>
          </div>
        </div>
      </nav>

      {/* Hero Section */}
      <section className="pt-32 pb-20 px-4 relative overflow-hidden">
        <div className="absolute inset-0 overflow-hidden">
          <div className="absolute -top-40 -right-40 w-80 h-80 bg-blue-500/20 rounded-full blur-3xl"></div>
          <div className="absolute -bottom-40 -left-40 w-80 h-80 bg-purple-500/20 rounded-full blur-3xl"></div>
        </div>

        <div className="max-w-4xl mx-auto text-center relative z-10">
          <h1 className="text-5xl md:text-7xl font-bold mb-6 bg-gradient-to-r from-blue-400 via-purple-400 to-pink-400 bg-clip-text text-transparent">
            The Future of Business Management
          </h1>
          <p className="text-xl text-slate-300 mb-8 max-w-2xl mx-auto">
            Streamline operations, boost productivity, and drive growth with our intelligent platform designed for modern enterprises.
          </p>
          <div className="flex flex-col md:flex-row gap-4 justify-center">
            <button className="px-8 py-3 bg-gradient-to-r from-blue-500 to-purple-600 rounded-lg font-semibold hover:shadow-lg hover:shadow-blue-500/50 transition flex items-center justify-center gap-2">
              Start Free Trial <ArrowRight size={20} />
            </button>
            <button className="px-8 py-3 border-2 border-slate-400 rounded-lg hover:border-blue-400 transition">
              Watch Demo
            </button>
          </div>
        </div>
      </section>

      {/* Features Section */}
      <section className="py-20 px-4 max-w-6xl mx-auto">
        <h2 className="text-4xl font-bold mb-16 text-center">Powerful Features</h2>
        <div className="grid md:grid-cols-4 gap-6">
          {features.map((feature, idx) => {
            const Icon = feature.icon;
            return (
              <div key={idx} className="p-6 rounded-xl bg-gradient-to-br from-slate-800 to-slate-700 hover:from-slate-700 hover:to-slate-600 transition group cursor-pointer">
                <Icon className="w-12 h-12 text-blue-400 mb-4 group-hover:scale-110 transition" />
                <h3 className="font-bold text-lg mb-2">{feature.title}</h3>
                <p className="text-slate-400">{feature.desc}</p>
              </div>
            );
          })}
        </div>
      </section>

      {/* Analytics Section */}
      <section className="py-20 px-4 max-w-6xl mx-auto">
        <h2 className="text-4xl font-bold mb-12 text-center">Analytics Dashboard</h2>
        
        <div className="grid md:grid-cols-2 gap-8 mb-8">
          <div className="bg-slate-800/50 backdrop-blur p-8 rounded-xl border border-slate-700">
            <h3 className="font-bold text-lg mb-6">Revenue Trends</h3>
            <ResponsiveContainer width="100%" height={250}>
              <LineChart data={chartData}>
                <CartesianGrid strokeDasharray="3 3" stroke="#334155" />
                <XAxis dataKey="month" stroke="#94a3b8" />
                <YAxis stroke="#94a3b8" />
                <Tooltip contentStyle={{ backgroundColor: '#1e293b', border: 'none', borderRadius: '8px' }} />
                <Line type="monotone" dataKey="revenue" stroke="#3b82f6" strokeWidth={2} dot={{ fill: '#3b82f6' }} />
              </LineChart>
            </ResponsiveContainer>
          </div>

          <div className="bg-slate-800/50 backdrop-blur p-8 rounded-xl border border-slate-700">
            <h3 className="font-bold text-lg mb-6">Performance Metrics</h3>
            <ResponsiveContainer width="100%" height={250}>
              <BarChart data={performanceData}>
                <CartesianGrid strokeDasharray="3 3" stroke="#334155" />
                <XAxis dataKey="name" stroke="#94a3b8" />
                <YAxis stroke="#94a3b8" />
                <Tooltip contentStyle={{ backgroundColor: '#1e293b', border: 'none', borderRadius: '8px' }} />
                <Bar dataKey="value" fill="#8b5cf6" radius={[8, 8, 0, 0]} />
              </BarChart>
            </ResponsiveContainer>
          </div>
        </div>

        <div className="grid md:grid-cols-4 gap-4">
          {[
            { label: 'Active Users', value: '12,584' },
            { label: 'Revenue (MTD)', value: '$48,392' },
            { label: 'Growth Rate', value: '+23.5%' },
            { label: 'Uptime', value: '99.99%' }
          ].map((stat, idx) => (
            <div key={idx} className="p-6 bg-gradient-to-br from-blue-500/10 to-purple-500/10 rounded-lg border border-blue-500/20">
              <p className="text-slate-400 mb-2">{stat.label}</p>
              <p className="text-3xl font-bold text-blue-400">{stat.value}</p>
            </div>
          ))}
        </div>
      </section>

      {/* Testimonials */}
      <section className="py-20 px-4 max-w-6xl mx-auto">
        <h2 className="text-4xl font-bold mb-12 text-center">What Our Clients Say</h2>
        <div className="grid md:grid-cols-3 gap-6">
          {testimonials.map((testimonial, idx) => (
            <div key={idx} className="p-6 bg-slate-800/50 rounded-xl border border-slate-700">
              <div className="flex gap-1 mb-4">
                {[...Array(5)].map((_, i) => <Star key={i} size={16} className="fill-yellow-400 text-yellow-400" />)}
              </div>
              <p className="text-slate-300 mb-4">"{testimonial.text}"</p>
              <div>
                <p className="font-semibold">{testimonial.name}</p>
                <p className="text-sm text-slate-400">{testimonial.role}</p>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* CTA Section */}
      <section className="py-20 px-4 relative overflow-hidden">
        <div className="absolute inset-0 bg-gradient-to-r from-blue-600/20 to-purple-600/20 blur-3xl"></div>
        <div className="max-w-4xl mx-auto text-center relative z-10 bg-gradient-to-r from-blue-500/10 to-purple-500/10 p-12 rounded-2xl border border-blue-500/20">
          <h2 className="text-4xl font-bold mb-6">Ready to Transform Your Business?</h2>
          <p className="text-xl text-slate-300 mb-8">Join thousands of companies already using BusinessHub</p>
          <button className="px-8 py-3 bg-gradient-to-r from-blue-500 to-purple-600 rounded-lg font-semibold hover:shadow-lg hover:shadow-blue-500/50 transition">
            Start Your Free Trial Today
          </button>
        </div>
      </section>

      {/* Footer */}
      <footer className="border-t border-slate-700 py-12 px-4">
        <div className="max-w-6xl mx-auto">
          <div className="grid md:grid-cols-4 gap-8 mb-8">
            <div>
              <p className="font-bold mb-4">Product</p>
              <ul className="space-y-2 text-slate-400">
                <li><a href="#" className="hover:text-blue-400">Features</a></li>
                <li><a href="#" className="hover:text-blue-400">Pricing</a></li>
                <li><a href="#" className="hover:text-blue-400">Security</a></li>
              </ul>
            </div>
            <div>
              <p className="font-bold mb-4">Company</p>
              <ul className="space-y-2 text-slate-400">
                <li><a href="#" className="hover:text-blue-400">About</a></li>
                <li><a href="#" className="hover:text-blue-400">Blog</a></li>
                <li><a href="#" className="hover:text-blue-400">Careers</a></li>
              </ul>
            </div>
            <div>
              <p className="font-bold mb-4">Resources</p>
              <ul className="space-y-2 text-slate-400">
                <li><a href="#" className="hover:text-blue-400">Documentation</a></li>
                <li><a href="#" className="hover:text-blue-400">API</a></li>
                <li><a href="#" className="hover:text-blue-400">Support</a></li>
              </ul>
            </div>
            <div>
              <p className="font-bold mb-4">Legal</p>
              <ul className="space-y-2 text-slate-400">
                <li><a href="#" className="hover:text-blue-400">Privacy</a></li>
                <li><a href="#" className="hover:text-blue-400">Terms</a></li>
                <li><a href="#" className="hover:text-blue-400">Contact</a></li>
              </ul>
            </div>
          </div>
          <div className="border-t border-slate-700 pt-8 text-center text-slate-400">
            <p>&copy; BusinessHub. All rights reserved.</p>
          </div>
        </div>
      </footer>
    </div>
  );
}
