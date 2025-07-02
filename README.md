const EditTaskModal = ({ isOpen, onClose, task, onSave }) => {
    const [editedTitle, setEditedTitle] = useState(task.title);
    const [editedDescription, setEditedDescription] = useState(task.description);
    const [editedPriority, setEditedPriority] = useState(task.priority);
    const [editedDueDate, setEditedDueDate] = useState(task.dueDate);

    useEffect(() => {
        setEditedTitle(task.title);
        setEditedDescription(task.description);
        setEditedPriority(task.priority);
        setEditedDueDate(task.dueDate);
    }, [task]);

    const handleSubmit = (e) => {
        e.preventDefault();
        onSave({
            id: task.id,
            title: editedTitle,
            description: editedDescription,
            priority: editedPriority,
            dueDate: editedDueDate,
            completed: task.completed,
            createdAt: task.createdAt,
        });
    };

    return (
        <Modal isOpen={isOpen} onClose={onClose} title="Edit Task">
            <form onSubmit={handleSubmit} className="space-y-4">
                <input
                    type="text"
                    value={editedTitle}
                    onChange={(e) => setEditedTitle(e.target.value)}
                    placeholder="Task Title"
                    className="w-full p-3 bg-gray-100 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-lg"
                    required
                />
                <input
                    type="text"
                    value={editedDescription}
                    onChange={(e) => setEditedDescription(e.target.value)}
                    placeholder="Description"
                    className="w-full p-3 bg-gray-100 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-lg"
                />
                <select
                    value={editedPriority}
                    onChange={(e) => setEditedPriority(e.target.value)}
                    className="w-full p-3 bg-gray-100 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-lg"
                >
                    <option value="low">Low Priority</option>
                    <option value="medium">Medium Priority</option>
                    <option value="high">High Priority</option>
                </select>
                <input
                    type="date"
                    value={editedDueDate}
                    onChange={(e) => setEditedDueDate(e.target.value)}
                    className="w-full p-3 bg-gray-100 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-lg"
                />
                <div className="flex justify-end gap-2">
                    <button
                        type="button"
                        onClick={onClose}
                        className="px-4 py-2 bg-gray-300 dark:bg-gray-600 text-gray-800 dark:text-white rounded-lg"
                    >
                        Cancel
                    </button>
                    <button
                        type="submit"
                        className="px-4 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700"
                    >
                        Save
                    </button>
                </div>
            </form>
        </Modal>
    );
};
